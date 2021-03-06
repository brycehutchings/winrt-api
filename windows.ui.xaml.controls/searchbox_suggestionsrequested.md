---
-api-id: E:Windows.UI.Xaml.Controls.SearchBox.SuggestionsRequested
-api-type: winrt event
---

<!-- Event syntax
public event Windows.Foundation.TypedEventHandler SuggestionsRequested<Windows.UI.Xaml.Controls.SearchBox,  Windows.UI.Xaml.Controls.SearchBoxSuggestionsRequestedEventArgs>
-->

# Windows.UI.Xaml.Controls.SearchBox.SuggestionsRequested

## -description
Occurs when the user's query text changes and the app needs to provide new suggestions to display in the search pane.

## -xaml-syntax
```xaml
<SearchBox SuggestionsRequested="eventhandler"/>
```


## -remarks
You can get suggestions from several sources:


+ You can define them yourself. For example, you could create a list of car manufacturers.
+ You can get them from Windows if your app searches local files.
+ You can get them from a web service or server.


For user experience guidelines for displaying suggestions, see [Guidelines and checklist for search](http://msdn.microsoft.com/library/c328faa3-f6ae-4970-8372-b413f1290c39).

You can use [LocalContentSuggestionSettings](../windows.applicationmodel.search/localcontentsuggestionsettings.md) to add suggestions, based on local files from Windows, in only a few lines of code. Alternatively, you can register for the search box control's [SuggestionsRequested](searchbox_suggestionsrequested.md) event and build your own list of suggestions that is made up of suggestions you retrieved from another source (like a locally-defined list or a web service).

For code examples that show how to add search suggestions, download the [SearchBox control sample](http://go.microsoft.com/fwlink/p/?LinkID=310082). The sample demonstrates how to add search suggestions by using all three possible sources, and how to add suggestions for East Asian languages by using alternate forms of the query text generated by an Input Method Editor (IME). (We recommend using query text alternatives if your app will be used by Japanese or Chinese users.)

### Types of search suggestions

There are two types of suggestions your app can display: suggestions that help users refine a query (query suggestions), and suggestions that are actual results of a query (result suggestions). You may choose to display either or both types of suggestions.

If you provide query suggestions and the user selects one, your app should respond by displaying results for the selected, refined query in your app's search results page.

If you provide result suggestions, you must also register a [ResultSuggestionChosen](searchbox_resultsuggestionchosen.md) event handler so that you can respond when the user selects one of your result suggestions and you can display the result to the user.

### Displaying app-provided suggestions

After you obtain suggestions, you display them by adding them to the [SearchSuggestionsRequest](../windows.applicationmodel.search/searchsuggestionsrequest.md).[SearchSuggestionCollection](../windows.applicationmodel.search/searchsuggestioncollection.md).

If you choose to display both query suggestions and result suggestions, you should group the suggestions by suggestion type (query or result) and separate the groups using [AppendSearchSeparator](../windows.applicationmodel.search/searchsuggestioncollection_appendsearchseparator.md). Each separator takes the place of a suggestion and must be followed by at least one suggestion, decreasing the number of suggestions that you can display.

The maximum length of all of the textual fields in a suggestion (such as text, detail text, and image alt text) is 512 characters.

To learn more about using suggestions to create a good search experience for your users in [Guidelines and checklist for search](http://msdn.microsoft.com/library/c328faa3-f6ae-4970-8372-b413f1290c39).

### Handling the SuggestionsRequested event asynchronously

If you want to respond to the [SuggestionsRequested](searchbox_suggestionsrequested.md) event asynchronously, you must obtain a [SearchSuggestionsRequestDeferral](../windows.applicationmodel.search/searchsuggestionsrequestdeferral.md) object before you edit the suggestion list. Here's an example from [Quickstart: Adding search to an app](http://msdn.microsoft.com/library/9fa49c2a-5237-4432-aa93-0829bdc9dfe0) that shows how:

```csharp
        public async static void SearchBox_SuggestionsRequested(
            SearchBox sender, 
            SearchBoxSuggestionsRequestedEventArgs args)
        {

            // This object lets us edit the SearchSuggestionCollection asynchronously. 
            var deferral = args.Request.GetDeferral();

            try { 

                // Retrieve the system-supplied suggestions.
                var suggestions = args.Request.SearchSuggestionCollection;
           
                var groups = await SampleDataSource.GetGroupsAsync();
                foreach (var group in groups)
                {
                    var matchingItems = group.Items.Where(
                        item => item.Title.StartsWith(
                            args.QueryText, StringComparison.CurrentCultureIgnoreCase));

                    foreach (var item in matchingItems)
                    {
                        suggestions.AppendQuerySuggestion(item.Title);
                    }
                }
            
                foreach (string alternative in args.LinguisticDetails.QueryTextAlternatives)
                {
                    if (alternative.StartsWith(
                        args.QueryText, StringComparison.CurrentCultureIgnoreCase))
                    {
                        suggestions.AppendQuerySuggestion(alternative); 
                    }
                }
            }
            finally {
                deferral.Complete();
            }

        }
```



## -examples

## -see-also
[Quickstart: Adding search to an app](http://msdn.microsoft.com/library/9fa49c2a-5237-4432-aa93-0829bdc9dfe0)
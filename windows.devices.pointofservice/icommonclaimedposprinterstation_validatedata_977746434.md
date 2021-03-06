---
-api-id: M:Windows.Devices.PointOfService.ICommonClaimedPosPrinterStation.ValidateData(System.String)
-api-type: winrt method
---

<!-- Method syntax
public bool ValidateData(System.String data)
-->

# Windows.Devices.PointOfService.ICommonClaimedPosPrinterStation.ValidateData

## -description
Determines whether a data sequence, possibly including one or more escape sequences, is valid for the printer station, before you use that data sequence when you call the [IPosPrinterJob.Print](iposprinterjob_print.md) and [IPosPrinterJob.ExecuteAsync](iposprinterjob_executeasync.md) methods.

## -parameters
### -param data
The data sequence that you want to validate before you use it with the [IPosPrinterJob.Print](iposprinterjob_print.md) method. This sequence may include printable data and escape sequences.

If the sequence is not valid, and you use it with [IPosPrinterJob.Print](iposprinterjob_print.md) anyways, the job fails when you run it with [IPosPrinterJob.ExecuteAsync](iposprinterjob_executeasync.md). You cannot remove a print instruction that uses an invalid data sequence after you add the instruction to the job with [IPosPrinterJob.Print](iposprinterjob_print.md).

## -returns
True if the data passes validation; otherwise false.

## -remarks

## -examples

## -see-also
[IPosPrinterJob.Print](iposprinterjob_print.md), [IPosPrinterJob.ExecuteAsync](iposprinterjob_executeasync.md), [ClaimedJournalPrinter.ValidateData](claimedjournalprinter_validatedata.md), [ClaimedReceiptPrinter.ValidateData](claimedreceiptprinter_validatedata.md), [ClaimedSlipPrinter.ValidateData](claimedslipprinter_validatedata.md)
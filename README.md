# PLM Data Health

Prototype for LOEWE merchandising. Two views on the PLM material export:

**Missing data.** Which fields are empty (price, MOQ, lead time…), the gaps by field and by supplier, and a chase list to send.

**Cross-check.** Compares the PLM export with a **Panorama** export and the **merch PowerPoint**, matched by material code, and lists what to resolve:
- **Different values**: price, composition, lead time, MOQ, supplier… that don't agree between sources (with the row or slide where each value comes from).
- **Fill PLM gap**: the PLM field is empty but Panorama or the deck has the value.
- **Empty elsewhere**: filled in PLM, empty (or "TBC") in another source.
- **Code not found**: in PLM but not in Panorama, or in Panorama / the deck but not in PLM, with a typo suggestion when two digits look swapped.

Formatting differences are not flagged: `12,50 €` = `12.5`, `98% CO 2% EA` = `Cotton 98%, elastane 2%`, `IT` = `Italy`, `9 wks` = `9`. Codes missing from the deck aren't flagged either, since a deck only shows a selection.

Columns are matched to PLM fields automatically (English, French, Spanish, Italian headers) and can be changed under **Fields compared**. Results can be copied for Excel or downloaded as an Excel report (summary + filterable list).

## Files it reads
- **PLM / Panorama:** .xlsx, .xls or .csv. For Panorama, the sheet, header row and code column are found automatically (title rows above the header are fine).
- **PowerPoint:** .pptx. Codes and values are read from tables (one material per row or per column) and from text boxes such as `Price: € 45.00 /m` under a code. Hidden slides are skipped.

Every file is read in the browser and is never uploaded.

## Try it
Opens on **invented sample data** for all three sources. `sample-data/` has invented files to load by hand: `Sample_PLM_export_Loewe_FAKE.xlsx`, `Sample_Panorama_export_FAKE.xlsx`, `Sample_merch_deck_FAKE.pptx`. Link straight to the cross-check with `#cross-check`.

## Tech
Single static file (`index.html`), no server. Libraries from cdnjs: SheetJS 0.18.5 (Excel read/write) and JSZip 3.10.1 (loaded only when a .pptx is opened). For internal hosting, vendor both next to `index.html`.

## To check with the team
- What Panorama exports look like (sheet layout, column names, code format) and how often they're pulled.
- Whether the deck values to check are always in tables, or also in free text boxes.
- Which tolerance is acceptable on prices (currently 0.5%).

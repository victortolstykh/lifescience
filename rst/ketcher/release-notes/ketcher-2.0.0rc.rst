Ketcher 2.0.0beta
#################

*3 May 2018*

*******
Summary
*******

We are glad to announce that a new Ketcher version **2.0.0 Release Candidate 1** is released. 

`Source code <https://github.com/epam/ketcher/releases/tag/2.0.0-beta.1>`__

The Data S Group descriptor can't be moved on the canvas by click and drag with Selection Tool.

The SGroup window doesn't open when user clicks the descriptor with Selection Tool.


Firefox: the images of templates in the Template Library display incorrectly (huge).

Need to remove the hydragens from terminal atoms in aromatic bonds until the ring is not closed.


EPMLSOPKET-1244 Create folder "3D Structures" in the Template Library.

EPMLSOPKET-1244 Create SDF-file with 3D Structures.
Add folder with 3D-structures in Template library.
Update the system of modules from CommonJS to ES6-modules.


Incorrect behavior after paste action



IE: Selection disappears from the template in the Template library when user opens the "Edit" window and then clicks "Cancel".



S Group: Error message appears in the Dev console when user selects the part of one SGroup and the whole another SGroup and then clicks Undo.



Two R-labels are enlarged when user moves the cursor over any R-Label except R1.




The opened expanded tool list doesn't contract



All objects disappear when user pastes the copied/cup Plus sign


Green circle contour should appear around atom when user accurately moves another atom to this one to fuse the structures


Settings - Open from file


Settings: expand/contract of the accordions



When user copies/cuts elements, taps ctrl+v and then clicks Undo button (ctrl+z) without attaching a copied element to the canvas, error message appears in the Dev console


Error message appears in Dev console when user moves the structure(s) which contains closely spaced bonds


Add fuse possibility verification when user creates the structure with closely spaced atoms

Chiral: Error message appears in the Dev console when user removes Chiral flag from the structure and then tries to move the structure on the canvas.

Saved files have a wrong expansion.


It is impossible to apply S-group to whole structure when another S-Group is applied to the part of this structure.


Error message appears in the developer console when user deletes the atom with descriptors and then clicks Undo buttons.

Selection on the descriptors doesn't disappear when user applies any other tool.

Incorrect application behavior if Reset to Select Tool is ON.

Atom stays selected when user applies another tool further.


InChi AuxInfo: & Enantiomer structure is rendered with chiral flag


Attachment atom and bond changes randomly when user clicks in the empty field around template in the "Edit" window in the Template library.

Structure flips incorrectly relative to the selected bond by horisontal and vertical Flips.


Attachment point for extended atom from periodic table doesn't display on the canvas.


Error message appears in the developer console when user opens any application window and then clicks "cancel" button.



S-Group descriptors run over the structure when user selects descriptors from "multifragment" context for the group of atoms in the structure and click ctrl+d.

R-Label button in the "R-Group" window doesn't work when user clicks at the left or right edge of this button.

R-Group Logic: the condition "Always" is shown as selected when user saves or cuts/pastes R-Group members with other conditions.


Inexplicit error messages in the fields "Atom" in "Label Edit" window and "Occurrence" in the "R-Group Logic" window.



R-fragment label isn't highlighted in "R-Group" window when user saves or cuts/copies/pastes the structure.


Template with Chiral flag doesn't move on the canvas when user choose ON in "Do not show the Chiral flag" in Settings


X-button displays incorrectly in the R-Group Label window when user moves the cursor over it.













When user removes r-group label from the atom in the structure, carbon atom, which replaced the r-group label, displays incorrectly.


Error message appears in the Developer Console when user clicks any Tool twice.

Context of data S-Group is changed from "Atom" to "Bond" when user sprouts the bond from atom with applied S-Group data.


Incorrect application behavior when user tries to save incorrect Multiple S-Group as template.

Template could not be added to any S-group internal atom.


Structure's selection by Selection tool disappears when user clicks S-Group tool or Data S-group tool.













User Template with R-member renamed after user refreshes application




































Stereochemistry Checker



























Atom should not be replaced if user doesn't choose R-label.






















Change api 'convert' for Extended SMILES
Schemify Save dialog
Add the possibility to save structure with necessary filename and add "Filename" field in the "Save Structure" window.



Green circle selection contour stays on the structure when user moves the cursor over scrollbars.












Incorrect header and footer in pop-up windows
Correct tests to use the docker
Correct tests for new version of Ketcher
Check-boxes in "Settings" menu in the "Check Structure" window cannot be unchecked.


















Chiral flag should be display on the canvas if at least one structure has Chiral flag.














"Chiral flag" checkbox should be added to "Settings" menu in "Check Structure" window.

The structures of the reaction couldn't be fused to each other after cut/paste this reaction.















Erase Tool: After click Esc button rectangle is appeared





























[IE]: Reaction arrow doesn't display on the canvas in Dev.









"Chiral" flag becomes bold after any user's action.
















The size of "Template Edit" window decreases when user taps "space" button in "Template name" field.














Set up CI to run tests with parameter passing
"Unsaturated", "Exact Change" checkboxes in Atom Properties window and checkboxes in Attachment Points window become checked/unchecked when user clicks somewhere near checkboxes.



















Application behavior differs in different browsers if Russian keyboard profile is activated.

[Chrome]: The error message tooltip doesn't appear when the cursor is out of the field with incorrect data.


















EPMLSOPKET-1058 Validation test for correctness of the display of atoms
[Edge40]: Ketcher reboots after changing Font type in Settings menu.














Unnecessary hydrogens appear after the Aromatize action











Descriptors are save trace of last position after undo
















A part of structures with closely spaced atoms cannot be moved with Rectangle Selection Tool

























Structure disappears from the screen when user drags it to any other place on the canvas


























Automated tests for Chain Tool
Cut/Copy are unavailible via menu at Edge 40































EPMLSOPKET-1058 Validation test for Bond Property
Automated tests for Bond Property Tool
Automated tests for Toolbox buttons displaying.
Automated tests for Bond Tool
EPMLSOPKET-1054 Correcting 3D Viewer tests
EPMLSOPKET-1054 Correcting Mapping Tool tests
EPMLSOPKET-1054 Correcting Atom Tool tests
Describe a chemically-useful way of determining relevance of derivatives
EPMLSOPKET-1058 Validation test for aromatic state of cyclic structure
EPMLSOPKET-1054 Correcting test "Server-operation with empty canvas"
EPMLSOPKET-1054 Correcting test "Aromatic structure can be aromatized and dearomatized"
EPMLSOPKET-1054 Correcting test "Non-aromatic structure cannot be aromatized and dearomatized"
EPMLSOPKET-1058 Partial screenshot for validation tests
EPMLSOPKET-1054 Correcting test "Erase Tool - icon and tooltips"
EPMLSOPKET-1054 Correcting test "Clean - bonds length"
Change tests that use screenshots
Edge(Template Library): incorrectly displaying symbol in the "Label" and "Atom" fields.































EPMLSOPKET-793 Imago version: Add UI element



EPMLSOPKET-793 Server: add imago_name parameter to /imago/uploads API call to switch between Imago versions

































Subscript Style for the numbers in the 'Chemical Formula' field













The mapping numbers should be rendered near the alias and pseudoatoms













Incorrect Clean-Layout for Rings


















Incorrect editing of the atom with attachment point



























Tool name and info about hot key for the Rgroup Fragment Tool overlap each other





User should be able to enter the correct '2-' value for the charge















Rgroup dialog schemify and redux


Information about isotopes in the 'Chemical Formula' field













Calculated Values for hydrogen























Atom coloring





























Continuous rotation of the templates and bonds

















CLONE - R-Group window appears when user clicks the scroll bar or scroll box
















Error message for the Save in SMILE format for the Rgroup member





















[Import From Image]: possibility to select Imago version




The Auto-Mapping action removes the Chiral flag



The 'cyclic' Rgroup definition should be forbidden






Incorrect SMILE rendering












Chiral flag persists on the canvas after delete or cut structure























Implement the ability to flip object selection in selection tools
Info about R/S labels appears in cml-file if the Rgroup fragment is present on the canvas
















Warning about the changing of the stereocenter after the strong 3D rotation

















Stricter ES6/React rules
Validate format conversion (warning messages)














Atom’s charge record in the 'Atom Propeties' dialog





















Saving of R-group members as smile-files
























The moving of the reaction after using of Auto-Mapping Tool





























The sprouted bonds should not be included into the previously created Data S-group



















'No errors found' message is present in the 'Structure Check' window for the structure with invalid valence

**New features and improvements**: 

* Add the possibility to Save structure as Extended SMILE

* Incorrect rendering (in Marvin) Ketcher SMILES for AND Enantiomer 

* Create saveSmiles() for Ketcher 

* Change the Bond type for several bonds at the same time 

* Structure can be fused bond to bond 

* Moving the structure with attached data 

* The 'cyclic' Rgroup definition should be forbidden 

* Problem with rendering a few condensed benzene rings 

* Add the possibility to save structure with necessary filename and add "Filename" field in the "Save Structure" window. 

* Include AuxInfo in InChI String 

* Templates for reaction



**Bugfixes**:

* Reaction Mapping Tool doesn't work after auto-mapping tool. 

* "Erase" doesn't delete selected structures when user crosses the scrollbars. 

* Incorrect order of "OK" and "Cancel" buttons in the "Settings" window. 

* The hyphen in the SMILES string for the aromatic structures 

* The application buttons are rendered incorrectly 

* [Edge40]: Double "Cancel" appears in "Label Edit" menu after adding template from Template Library. 

* The 'Label Edit' window opens during the moving of the scroll box 

* Structure with Sgroup cannot be saved as template 

* Message doesn't appears when user tries to dearomatize the structure with query-bonds. 

* Some templates have incorrect attachment atom 

* [Edge40]: Ketcher reboots after adding R-Group to the structure with template from Template Library 

* Fragment/Rectangle Selection tool's focus disappeared after changing the screen size 

* Selection Tool: Lasso Selection tool becomes active on the Toolbar after copy/cut/paste with other Selection tool 

* Fragment Selection Tool: selection disappeared when user click the canvas keep pressing Shift key 

* [Cosmetic only] Misprint in the error message using paste tool 

* Fragment Selection Tool: uncomfortable selection 

* Multiple warning for the Selection Tools in the Dev Console 

* [Edit Templates]: incorrect rendering of the descriptors, reaction arrow and plus signs 

* Calculate CIP tool returns incorrect position type for s-group data 

* The joint bond of the fused fragment should be the same as the bond of the moved structure 

* Custom Templates:One atoms of the structure is not displayed in the "Label edit" window 

* Tool palette doesn't close 

* Valence error after the Aromatize action 

* Template structures appear on canvas without Chiral flag 

* Problems with Undo after some actions with structures with Sgroups 

* The Double bonds in the first fused benzene are changed with the Single one 

* The structure is moved without stereo labels and attached data 

* Chiral flag persists on the canvas after delete or cut structure 

* Unpredictable behavior of the Undo action for the pasted/inserted reaction 

* [All browsers] Incorrect Undo/Redo behavior 

* About window: text about Indigo version overlaps the 'Indigo Toolkit' text 

* The Stereo labels and Attached Data keep their positions after the Flip action 

* Templates appear without saved attached data 

* Structure doesn't save to template when user chooses any format except MDL Molfile 

* Ketcher hangs after user adds empty template to the canvas 

* Two structures with the same R-fragment Tool appeared as two separate structures inside different square brackets 

* Incorrect error message appears when "Filename" field in "Save Structure" window is empty. 

* The structures of the reaction are relocated relative to each other after save or cut/paste. 

* Selection tool's focus disappeared after copy/paste of reaction arrow. 

* Reaction is relocated on the canvas after saving in rxn-format. 

* Incorrect bond rendering after refactoring 

* Buttons "Open From File", "Cancel", "Save To File" and "Save To Templates" have different styles. 

* The button "Open From File" doesn't work when user clicks at this button before, below or after the text "Open From File". 

* R-Group window appears when user clicks the scroll bar or scroll box 

* The Rotation angle value should appear 

* Checker: warning about Chirality 



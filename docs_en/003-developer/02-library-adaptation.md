# Library Adaptation 

## Development and Debugging Method  

### Enable Developer Mode
Through `Menu > Settings > Developer Mode`, enable developer mode. At this time, a 🔁 icon will appear to the right of the `Library Manager` button in the lower left corner of the blockly workspace, which is used to manually reload the library after modifying the library source code.

### Install Library
You can first put the library template or your own created library in any location on the computer, such as `d:\lib-test`.
Then open the project in aily blockly, open the terminal, and input:
```
npm i d:\lib-test
```
You can install this library for this project.

### Reload Library
Click the 🔁 icon to the right of `Project Management` to reload the project. After loading, the new library will be displayed in the left menu.

### Modify Library
You can directly modify `node_modules\@aily-project\<library name>` in the project directory, and then reload in aily blockly to test;
You can also modify the original library under `d:\lib-test`, and then install the library again to test.

## Submit Library 
You can first fork this project to your personal repository. Then put your newly created library in it, and then submit a Pull request.
Contact Naihe col to merge, or wait for other project administrators to merge.  
After the merge is complete, it will be pushed to the npm repository, and all users can use your developed library.

## Multi-language Support  
You can add an i18n directory under the library directory to provide multi-language support for the library:
```
library-name  
 |- block.json             // aily blockly block file
 |- generator.js           // aily blockly generator file
 |- toolbox.json           // aily blockly toolbox file
 |- package.json           // npm package management file
 |- src.7z                 // Arduino library source file, please use 7z extreme compression and put it in the library
 |- readme.md              // Description file, if you use open source libraries, please explain
 |- i18n                   // Multi-language support
     |- en.json            // English
     |- zh_cn.json         // Simplified Chinese
     |- zh_tw.json         // Traditional Chinese
     |- xxxx.json          // Other languages
```

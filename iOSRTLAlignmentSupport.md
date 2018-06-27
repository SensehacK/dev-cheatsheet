# Reusable component for Text Alignment.

## Prerequisites: 

* Xcode IDE
* Mac OS 
* iTunes
* iOS Device


## Creation: 

### Step 1:
Use the singleton class file where it is imported everywhere in the project. For my example, I have "Utility.m" in objective C.

#### Utility class : 

//**AR
//Moving generic method here to use Singleton feature
//This is just calling TranslationDashboard method
-(NSInteger)getAlignment{
    return [[TranslationDashboard sharedManager] getAlignment];
}

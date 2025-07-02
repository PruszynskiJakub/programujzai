---
category: "[[Tool]]"
tags:
  - references
website: https://www.heyalice.app/
docs: https://heyalice.app/academy
---
# Specification Template  
> Ingest the information from this file, implement the Low-Level Tasks, and generate the code that will satisfy the High and Mid-Level Objectives.  
  
## High-Level Objective  
- Creating basic structure for a new feature  
  
## Mid-Level Objective  
- Create feature package  
- Create dummy screen  
- Create dummy screen model  
- Create di module  
- Include the module in the koin graph  
  
## Implementation Notes  
- [Important technical details - what are the important technical details?]  
- [Dependencies and requirements - what are the dependencies and requirements?]  
- [Coding standards to follow - what are the coding standards to follow?]  
- [Other technical guidance - what are other technical guidance?]  
  
## Context  
  
### Beginning context  
  
- composeApp/src/commonMain/kotlin/com/cardiapath/app/InitKoin.kt  
  
### Ending context  
  
- composeApp/src/commonMain/kotlin/com/cardiapath/app/InitKoin.kt  
- composeApp/src/commonMain/kotlin/com/cardiapath/app/feature/[featurename]/di/[featurename]  
  Module.kt]  
- composeApp/src/commonMain/kotlin/com/cardiapath/app/feature/[featurename]/[featurename]Screen.kt]  
- composeApp/src/commonMain/kotlin/com/cardiapath/app/feature/[featurename]/[featurename]  
  ScreenModel.kt]  
  
## Low-Level Tasks  
> Ordered from start to finish  
1. Ask for the feature name  
```aider  
Ask for the feature name to create, do nothing beyond that. Proceed only if you have the feature name.  
Follow the naming pattern for feature packages, classes or fields. Names in [..] are placeholders having the naming pattern.  
Example:  
[JohnDoe]Screen -> JohnDoeScreen  
```  
  
1. Create basic structure for a new feature  
```aider  
CREATE feature/[featurename]:  
    CREATE [FeatureName]Screen.kt:        ADD object [FeatureName]Screen: Screen with composable content ScreenPlaceholder("[FeatureName]"),    CREATE [FeatureName]ScreenModel.kt:        ADD class [FeatureName]ScreenModel(logger: Logger, val dispatchers: AppDispatchers): AppStateScreenModel<State>(State(), logger),        ADD inner data class State(val foo: String = "")    CREATE di/[FeatureName]Module.kt:        ADD val [featureName]Module = module { factory { [FeatureName]ScreenModel(dispatchers = get())} },        USE getLoggerWithTag("[FeatureName]Module") to inject logger    CREATE package designs```  
2. Initialize screen model on screen  
```aider  
    MODIFY fun Content() inside [FeatureName]Screen:        ADD val screenModel = getScreenModel<[FeatureName]ScreenModel>()```  
  
3. Add feature module to koin graph  
```aider  
    INCLUDE [featureName]Module in featuresModule ONLY if new feature files created.```
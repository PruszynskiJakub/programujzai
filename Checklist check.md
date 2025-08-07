---
category: "[[Tips & Tricks]]"
---
[[Claude Code]] 

Jedną ze skuteczniejszych technik zapewniających jakość wygenerowanego rozwiązania to moim zdaniem checklist'a.

Wypunktowane kroki na których których nam zależy.

Pozwala nam ominąć błędy kompilacyjne, testy, przeszukiwanie standardów i istniejących komponentów.

Przykład checklisty:

```
1. Verify if Atomic Design principles are applied @composeApp/src/commonMain/kotlin/com/healthfolder/v2/design_system/component/DesignSystem.kt  
2. Verify if the code build is using already created components @composeApp/src/commonMain/kotlin/com/healthfolder/v2/design_system/component  
3. Verify if the code build is using already created themes (Color.kt, Shapes.kt, Theme.kt, Typography.kt) @composeApp/src/commonMain/kotlin/com/healthfolder/v2/design_system/theme  
4. Verify if there are no hardcoded colors in the code. If yes - move it to @composeApp/src/commonMain/kotlin/com/healthfolder/v2/design_system/theme/Color.kt  
5. Verify if there are no hardcoded displayed texts in the code. If yes - create a new string resource in @composeApp/src/commonMain/kotlin/com/healthfolder/v2/core/common/localization/StringResources.kt` and proper values in translations `composeApp/src/commonMain/kotlin/com/healthfolder/v2/core/common/localization/translations  
6. If implementing / changing integration with Backend verify if the Serailisation is matching the Backend API documentation AI_DOCS/backend-swagger-docs.json  
7. Ensure all conventions have been applied from: @AI_DOCS/CONVENTIONS.md  
8. Make sure all created files are added to the git  
9. Application builds and runs properly  
10. Proper formatting applied: `./gradlew ktlintFormat`
```


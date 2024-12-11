# Main Application (main.dart)

This documentation provides an overview of the **main.dart** file, the entry point for the Virechana Karma Assessment App. It outlines the structure, key components, and functionalities implemented in the application.

---

## **Overview**

The `main.dart` file:

- Initializes the app and sets up necessary dependencies.
- Defines the main navigation structure using `PageView`.
- Integrates with the Google Sheets API for data storage.
- Provides an intuitive user interface for the assessment process.

---

## **Key Components**

**Main Entry Point**

- Initializes the app and ensures necessary dependencies are ready.
  **VirechanaApp Class**
- Configures the app theme and sets the home screen.
  **FormNavigator Class**
- Implements a `PageView` to navigate between assessment screens.

---

## **Code Breakdown**

### **App Initialization**

```
Future main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await VirechanaSheetApi.init();
  runApp(
    ProviderScope(
      child: VirechanaApp(),
    ),
  );
}
```

- **`WidgetsFlutterBinding.ensureInitialized()`**: Ensures Flutter bindings are initialized before running the app.
- **`VirechanaSheetApi.init()`**: Initializes the Google Sheets API for data integration.
- **`ProviderScope`**: Wraps the app to enable Riverpod state management.

---

### **VirechanaApp Class**

```
class VirechanaApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Virechana Karma App',
      theme: ThemeData(primarySwatch: Colors.teal),
      home: FormNavigator(),
    );
  }
}
```

- **`MaterialApp`**: Provides the app's configuration and navigation.
  - **`debugShowCheckedModeBanner`**: Disabled for a cleaner interface.
  - **`title`**: Sets the app's title.
  - **`theme`**: Configures the app's theme with a teal color scheme.
  - **`home`**: Sets the starting page to `FormNavigator`.

---

### **FormNavigator Class**

The `FormNavigator` class implements the main navigation for the assessment process using a `PageView`.

#### **PageView Implementation**

```
class FormNavigator extends StatefulWidget {
  @override
  _FormNavigatorState createState() => _FormNavigatorState();
}

class _FormNavigatorState extends State<FormNavigator> {
  final PageController _pageController = PageController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Virechana Karma Assessment')),
      body: PageView(
        controller: _pageController,
        physics: NeverScrollableScrollPhysics(),
        children: [
          PatientDetailsPage(controller: _pageController),
          PurvakarmaPage(controller: _pageController),
          PradhanaKarmaPage(controller: _pageController),
          ShuddhiAssessmentPage(controller: _pageController),
          SamyakYogaLakshanaPage(controller: _pageController),
          AyogaOfVirechnaPage(controller: _pageController),
          AtiyogaOfVirechanaPage(controller: _pageController),
          PostProcedurePage(controller: _pageController),
          SummaryPage(controller: _pageController),
        ],
      ),
    );
  }
}
```

#### **Key Features**

**PageController**

- Manages navigation between pages programmatically.

**`PageView`**

- Displays the assessment screens.
- **`NeverScrollableScrollPhysics`**: Prevents manual scrolling to enforce the sequential flow of pages.

**Children Pages**

Pages included:

- **PatientDetailsPage**: Collects basic patient information.
- **PurvakarmaPage**: Gathers pre-assessment metrics.
- **PradhanaKarmaPage**: Records procedural details.
- **ShuddhiAssessmentPage**: Evaluates the effectiveness of the procedure.
- **SamyakYogaLakshanaPage**: Captures `Samyak Yoga` characteristics.
- **AyogaOfVirechnaPage**: Lists symptoms indicating Ayoga.
- **AtiyogaOfVirechanaPage**: Lists symptoms indicating Atiyoga.
- **PostProcedurePage**: Records post-procedure observations.
- **SummaryPage**: Consolidates all collected data for review and submission.

---

## **Navigation Flow**

The navigation between pages is controlled programmatically using `PageController`. Each page:

- Receives the `PageController` instance as a parameter.
- Navigates to the next page upon user action.

---

## **Integration with Google Sheets**

The `VirechanaSheetApi` is initialized at the start to allow seamless data submission to Google Sheets:

```
await VirechanaSheetApi.init();
```

---

## **Conclusion**

The **main.dart** file serves as the backbone of the Virechana Assessment App. It initializes the app, sets up dependencies, and defines the navigation flow using `PageView`. With its clean and modular design, the app ensures a seamless and user-friendly experience for conducting assessments.


![Screenshot 2025-05-20 110115](https://github.com/user-attachments/assets/be6a96b6-4a61-44bd-b78f-342443538323)

## home_screen.dart
  ### homescreen class
  ``` sh
  class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});
  ```
  - Defines stateless widget
  ### scaffold layout
  ```sh
  return Scaffold(
    appBar: AppBar(
      title: const Text('Home Page'),
      centerTitle: true,
    ),
  ```
  - sets up basic UI
  ### List of notification buttons
  #### Default Notif
  ```sh
            OutlinedButton(
            onPressed: () async {
              await NotificationService.createNotification(
                id: 1,
                title: 'Default Notification',
                body: 'This is the body of the notification',
                summary: 'Small summary',
              );
            },
            child: const Text('Default Notification'),
          ),
  ```
  #### Notification with Summary
  ``` sh
   OutlinedButton(
            onPressed: () async {
              await NotificationService.createNotification(
                id: 2,
                title: 'Notification with Summary',
                body: 'This is the body of the notification',
                summary: 'Small summary',
                notificationLayout: NotificationLayout.Inbox,
              );
            },
            child: const Text('Notification with Summary'),
          ),
  ```
  #### Progress Bar Notification
  ```sh
  OutlinedButton(
            onPressed: () async {
              await NotificationService.createNotification(
                id: 3,
                title: 'Progress Bar Notification',
                body: 'This is the body of the notification',
                summary: 'Small summary',
                notificationLayout: NotificationLayout.ProgressBar,
              );
            },
            child: const Text('Progress Bar Notification'),
          ),
  ```
  #### Message Notif
  ```sh
  OutlinedButton(
              onPressed: () async {
                await NotificationService.createNotification(
                  id: 4,
                  title: 'Message Notification',
                  body: 'This is the body of the notification',
                  summary: 'Small summary',
                  notificationLayout: NotificationLayout.Messaging,
                );
              },
              child: const Text('Message Notification'),
            ),
  ```
  #### Big image notif
  ```sh
            OutlinedButton(
              onPressed: () async {
                await NotificationService.createNotification(
                  id: 5,
                  title: 'Big Image Notification',
                  body: 'This is the body of the notification',
                  summary: 'Small summary',
                  notificationLayout: NotificationLayout.BigPicture,
                  bigPicture: 'https://picsum.photos/300/200',
                );
              },
              child: const Text('Big Image Notification'),
            ),
  ```
  #### Action button notif
  ```sh
            OutlinedButton(
              onPressed: () async {
                await NotificationService.createNotification(
                  id: 6,
                  title: 'Action Button Notification',
                  body: 'This is the body of the notification',
                  payload: {'navigate': 'true'},
                  actionButtons: [
                    NotificationActionButton(
                      key: 'action_button',
                      label: 'Click me',
                      actionType: ActionType.Default,
                    ),
                  ],
                );
              },
              child: const Text('Action Button Notification'),
            ),
  ```
  #### Scheduled notif
  ```sh
            OutlinedButton(
              onPressed: () async {
                await NotificationService.createNotification(
                  id: 7,
                  title: 'Scheduled Notification',
                  body: 'This is the body of the notification',
                  scheduled: true,
                  interval: 5,
                );
              },
              child: const Text('Scheduled Notification'),
            ),
  ```

## second_screen.dart
  ### secondscreen class
    ```sh
    class SecondScreen extends StatelessWidget {
    const SecondScreen({super.key});
    ```
  - Declares stateless widget
  ### Scaffold layout
  ```sh
  return Scaffold(
    appBar: AppBar(
      title: const Text('Second Screen'),
      centerTitle: true,
    ),
  ```
  - builds the basic layout
  ### Body content
  ```sh
        body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
  ```
  - centers content
  - uses column to stack child widget
  ### widgets inside column
  ```sh
    const Text('This is the second screen from the notification!'),
    const SizedBox(height: 20),
    OutlinedButton(
      onPressed: () {
        Navigator.pop(context);
      },
      child: const Text('Go to Home'),
    ),
  ```
  - displays message
  - adds vertical spacing using SizedBox
  - Adds button

## notification_service.dart
  ### notificationservice class
  ```sh
  class NotificationService {
  ```
  - utility class to handle notif initialization
  ### initializenotification
  ```sh
  static Future<void> initializeNotification() async {
  ```
  - defines channel and channel group
  - requests permission
  ### notif listeners
  ```sh
  setListeners(...)
  ```
  - _onNotificationCreateMethod: Logs when a notification is created

  - _onNotificationDisplayedMethod: Logs when a notification is shown

  - _onDismissActionReceivedMethod: Logs when a notification is dismissed

  - _onActionReceivedMethod: Executes logic when the notification is tapped
  ### _onActionReceivedMethod
  ```sh
  if (payload['navigate'] == 'true') {
  Navigator.push(...);
  }
  ```
  - Navigates to SecondScreen using the app’s global navigatorKey
  ### createNotification()
  ```sh
  static Future<void> createNotification({...})
  ```
  - creates notif with customizable ID, title, body; summary, layout, category, image, payload; action buttons and scheduling options
  ## main.dart
  ### main() function
  ```sh
  void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await NotificationService.initializeNotification();
  runApp(const MyApp());
  }
  ```
  - initalizes flutter binding
  - calls notif initialization method
  - runs the app
  ### MyApp class
  ```sh
  class MyApp extends StatelessWidget {
  const MyApp({super.key});
  ```
  - Defines root widget of the app as stateless widget
  ### Global Navigator Key
  ```sh
  static GlobalKey<NavigatorState> navigatorKey = GlobalKey<NavigatorState>();
  ```
  - allows global access to navigation
  ### build()
  ```sh
  return MaterialApp(
    title: 'Notification Demo',
    routes: {
      'home': (context) => const HomeScreen(),
      'second': (context) => const SecondScreen(),
    },
    initialRoute: 'home',
    navigatorKey: navigatorKey,
  );
  ```
  - sets up main UI

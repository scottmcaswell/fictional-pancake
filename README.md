<activity 
        android:name=".MainActivity"
        android:label="@string/app_name"
        android:launchMode="singleInstance"
        android:windowSoftInputMode="adjustPan" >
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />

            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
</activity>src/hotspotimport android.app.Notification;
import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.Service;
import android.content.Context;
import android.content.Intent;
import android.os.IBinder;
import android.util.Log;

public class NotisyncListenerService extends Service {
    private static final String TAG = "NotisyncListenerService";
    private static final String CHANNEL_ID = "notisync_channel";
    private static final int NOTIFICATION_ID = 1;

    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        super.onCreate();
        Log.d(TAG, "Service created");

        // Create Notification Channel (for Android O and above)
        createNotificationChannel();
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        Log.d(TAG, "Service started");

        // Start listening for notifications (implement your logic here)
        // This is a placeholder. You'll need to implement your actual notification listening logic here.
        // This might involve using Accessibility services, NotificationListeners, or other methods 
        // depending on your specific requirements.

        // Example: Send a notification to indicate the service is running
        showNotification("Notisync Listener Service Running");

        return START_STICKY; // Restart service if killed
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        Log.d(TAG, "Service destroyed");
    }

    private void createNotificationChannel() {
        if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.O) {
            CharSequence name = getString(R.string.channel_name); // Replace with your channel name
            String description = getString(R.string.channel_description); // Replace with your channel description

            int importance = NotificationManager.IMPORTANCE_DEFAULT;
            NotificationChannel channel = new NotificationChannel(CHANNEL_ID, name, importance);
            channel.setDescription(description);

            NotificationManager notificationManager = getSystemService(NotificationManager.class);
            notificationManager.createNotificationChannel(channel);
        }
    }

    private void showNotification(String message) {
        NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);

        Notification.Builder builder = new Notification.Builder(this, CHANNEL_ID)
                .setContentTitle("Notisync Listener")
                .setContentText(message)
                .setSmallIcon(R.drawable.ic_notification) // Replace with your icon
                .setAutoCancel(true);

        notificationManager.notify(NOTIFICATION_ID, builder.build());
    }
}
docs/install_linux.mdWere offering mobile cleaning and auto detailing 

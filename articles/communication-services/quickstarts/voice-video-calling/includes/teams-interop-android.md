---
title: Szybki Start — Dołącz do spotkania zespołów z poziomu aplikacji systemu Android
description: W tym samouczku dowiesz się, jak przyłączyć się do spotkania zespołów przy użyciu biblioteki klienta wywołującego usługi Azure Communications Services dla systemu Android
author: chpalm
ms.author: mikben
ms.date: 03/10/2021
ms.topic: quickstart
ms.service: azure-communication-services
ms.openlocfilehash: 82e64af5cec8641abacf5afa323fc38382a124c4
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 03/16/2021
ms.locfileid: "103488011"
---
W tym przewodniku szybki start dowiesz się, jak przyłączyć się do spotkania zespołów przy użyciu biblioteki klienta wywołującego usługi Azure Communications Services dla systemu Android.

## <a name="prerequisites"></a>Wymagania wstępne

- Działająca [usługa komunikacyjna wywołująca aplikację dla systemu Android](../getting-started-with-calling.md).
- [Wdrożenie zespołów](/deployoffice/teams-install).


## <a name="add-the-teams-ui-controls"></a>Dodawanie formantów interfejsu użytkownika zespołów

Zastąp kod w activity_main.xml następującym fragmentem kodu. Pole tekstowe zostanie użyte do wprowadzenia kontekstu spotkania zespołów, a przycisk zostanie użyty w celu dołączenia do określonego spotkania:

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/teams_meeting_link"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="Teams meeting link"
        android:inputType="textUri"
        android:layout_marginTop="100dp"
        android:layout_marginHorizontal="20dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="70dp"
        android:gravity="center"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent">

        <Button
            android:id="@+id/join_meeting_button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Join Meeting" />

        <Button
            android:id="@+id/hangup_button"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hangup" />

    </LinearLayout>

    <TextView
        android:id="@+id/call_status_bar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="40dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

    <TextView
        android:id="@+id/recording_status_bar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="20dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

## <a name="enable-the-teams-ui-controls"></a>Włączanie formantów interfejsu użytkownika zespołów

Zastąp zawartość `MainActivity.java` następującym fragmentem kodu:

```java

package com.contoso.acsquickstart;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.concurrent.ExecutionException;

import com.azure.android.communication.calling.Call;
import com.azure.android.communication.calling.CallAgent;
import com.azure.android.communication.calling.CallClient;
import com.azure.android.communication.calling.HangUpOptions;
import com.azure.android.communication.calling.JoinCallOptions;
import com.azure.android.communication.common.CommunicationTokenCredential;
import com.azure.android.communication.calling.TeamsMeetingLinkLocator;

public class MainActivity extends AppCompatActivity {
    private static final String[] allPermissions = new String[] { Manifest.permission.RECORD_AUDIO, Manifest.permission.CAMERA, Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.READ_PHONE_STATE };
    private static final String UserToken = "<User_Access_Token>";

    TextView callStatusBar;
    TextView recordingStatusBar;

    private CallAgent agent;
    private Call call;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        getAllPermissions();
        createAgent();

        Button joinMeetingButton = findViewById(R.id.join_meeting_button);
        joinMeetingButton.setOnClickListener(l -> joinTeamsMeeting());

        Button hangupButton = findViewById(R.id.hangup_button);
        hangupButton.setOnClickListener(l -> leaveMeeting());

        callStatusBar = findViewById(R.id.call_status_bar);
        recordingStatusBar = findViewById(R.id.recording_status_bar);
    }

    /**
     * Join Teams meeting
     */
    private void joinTeamsMeeting() {
        if (UserToken.startsWith("<")) {
            Toast.makeText(this, "Please enter token in source code", Toast.LENGTH_SHORT).show();
            return;
        }

        EditText calleeIdView = findViewById(R.id.teams_meeting_link);
        String meetingLink = calleeIdView.getText().toString();
        if (meetingLink.isEmpty()) {
            Toast.makeText(this, "Please enter Teams meeting link", Toast.LENGTH_SHORT).show();
            return;
        }

        JoinCallOptions options = new JoinCallOptions();
        TeamsMeetingLinkLocator teamsMeetingLinkLocator = new TeamsMeetingLinkLocator(meetingLink);
        call = agent.join(
                getApplicationContext(),
                teamsMeetingLinkLocator,
                options);
        call.addOnStateChangedListener(p -> setCallStatus(call.getState().toString()));
        call.addOnIsRecordingActiveChangedListener(p -> setRecordingStatus(call.isRecordingActive()));
    }

    /**
     * Leave from the meeting
     */
    private void leaveMeeting() {
        try {
            call.hangUp(new HangUpOptions()).get();
        } catch (ExecutionException | InterruptedException e) {
            Toast.makeText(this, "Unable to leave meeting", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * Create the call agent
     */
    private void createAgent() {
        try {
            CommunicationTokenCredential credential = new CommunicationTokenCredential(UserToken);
            agent = new CallClient().createCallAgent(getApplicationContext(), credential).get();
        } catch (Exception ex) {
            Toast.makeText(getApplicationContext(), "Failed to create call agent.", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * Request each required permission if the app doesn't already have it.
     */
    private void getAllPermissions() {
        ArrayList<String> permissionsToAskFor = new ArrayList<>();
        for (String permission : allPermissions) {
            if (ActivityCompat.checkSelfPermission(this, permission) != PackageManager.PERMISSION_GRANTED) {
                permissionsToAskFor.add(permission);
            }
        }
        if (!permissionsToAskFor.isEmpty()) {
            ActivityCompat.requestPermissions(this, permissionsToAskFor.toArray(new String[0]), 1);
        }
    }

    /**
     * Ensure all permissions were granted, otherwise inform the user permissions are missing.
     */
    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, int[] grantResults) {
        boolean allPermissionsGranted = true;
        for (int result : grantResults) {
            allPermissionsGranted &= (result == PackageManager.PERMISSION_GRANTED);
        }
        if (!allPermissionsGranted) {
            Toast.makeText(this, "All permissions are needed to make the call.", Toast.LENGTH_LONG).show();
            finish();
        }
    }

    /**
     * Shows call status in status bar
     */
    private void setCallStatus(String status) {
        runOnUiThread(() -> callStatusBar.setText(status));
    }

    /**
     * Shows recording status status bar
     */
    private void setRecordingStatus(boolean status) {
        if (status == true) {
            runOnUiThread(() -> recordingStatusBar.setText("This call is being recorded"));
        }
        else {
            runOnUiThread(() -> recordingStatusBar.setText(""));
        }
    }
}

```

## <a name="get-the-teams-meeting-link"></a>Pobierz link do spotkania dla zespołów

Link do spotkania zespołów można pobrać przy użyciu interfejsów API programu Graph. Jest to szczegółowo opisany w [dokumentacji programu Graph](/graph/api/onlinemeeting-createorget?tabs=http&view=graph-rest-beta).
Biblioteka klienta wywołującego usługę komunikacyjną akceptuje łącze do spotkania z pełnymi zespołami. Ten link jest zwracany jako część `onlineMeeting` zasobu, który jest dostępny w ramach [ `joinWebUrl` Właściwości](/graph/api/resources/onlinemeeting?view=graph-rest-beta). Wymagane informacje o spotkaniu można również uzyskać od adresu URL **spotkania przyłączenia** do zespołu, który zaprosił się w sobie.

## <a name="launch-the-app-and-join-teams-meeting"></a>Uruchom aplikację i Dołącz do spotkania zespołów

Aplikację można teraz uruchomić przy użyciu przycisku "Uruchom aplikację" na pasku narzędzi (Shift + F10). Powinien zostać wyświetlony następujący ekran:

:::image type="content" source="../media/android/acs-join-teams-meeting-quickstart.png" alt-text="Zrzut ekranu przedstawiający ukończoną aplikację.":::

Wstaw kontekst zespołów do pola tekstowego i naciśnij pozycję *Dołącz do spotkania* , aby dołączyć do zespołu spotkania z poziomu aplikacji usług komunikacyjnych.

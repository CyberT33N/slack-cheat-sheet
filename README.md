# Slack Cheat Sheet

<br><br>

## Bots
- **Free User können nur 10 Bots benutzen**

1. Gehe zu https://api.slack.com/ und melde dich mit deinem Slack-Konto an.
Klicke auf "Create New App". Wähle "From scratch" und gib deiner App einen Namen. Wähle auch den Slack-Workspace aus, in dem du die App entwickeln möchtest.

2. In den Einstellungen deiner App auf der Slack-API-Seite findest du das Menü "OAuth & Permissions". Hier kannst du Scopes hinzufügen, die deinem Bot bestimmte Rechte geben.
Füge im Abschnitt "Bot Token Scopes" die notwendigen Scopes hinzu, je nachdem, was dein Bot tun soll.
- chat:write

3. Im selben "OAuth & Permissions"-Bereich findest du oben einen Button "Install to Workspace". Durch Klicken auf diesen Button wird die App zu deinem Slack-Workspace hinzugefügt.
Nach der Installation wird dir ein Bot User OAuth Access Token angezeigt. Das ist dein SLACK_BOT_TOKEN.

4. Gehe zum Abschnitt "Basic Information" in den Einstellungen deiner App auf der Slack-API-Seite.
Scroll nach unten zum Abschnitt "App Credentials". Hier findest du dein Signing Secret.

5. Füge den Bot zum Kanal hinzu:
- Gehe zu Slack und navigiere zum Kanal, in dem du die Nachricht senden möchtest.
Füge den Bot als Mitglied hinzu, indem du /invite @<DeinBotName> im Nachrichtenfeld des Kanals eingibst. Ersetze <DeinBotName> mit dem Namen deines Bots.



<br><br>
<br><br>


### Node.js
```shell
npm install @slack/bolt @slack/web-api
```

```javascript
const { App } = require('@slack/bolt');

// Holt Ihre Bot-Token und Signing Secret von der Umgebung.
const botToken = process.env.SLACK_BOT_TOKEN;
const signingSecret = process.env.SLACK_SIGNING_SECRET;

const app = new App({
  token: botToken,
  signingSecret: signingSecret
});

// Starten Sie Ihre App
(async () => {
  await app.start(process.env.PORT || 3000);
  console.log('⚡️ Slack-Bolt-App läuft!');

  const channelId = 'YOUR_CHANNEL_ID'; // Ersetzen Sie dies durch Ihre Kanal-ID

    async function sendMessage(text) {
    try {
        // Verwenden Sie die `chat.postMessage` Methode, um eine Nachricht an einen Kanal zu senden
        const result = await app.client.chat.postMessage({
        token: botToken,
        channel: channelId,
        text: text
        });

        console.log(result);
    }
    catch (error) {
        console.error(error);
    }
    }

    // Senden einer Nachricht
    await sendMessage('Hallo Welt!');
})();
```

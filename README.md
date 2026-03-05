// --- 1. म्यूजिक, वेरिएबल और JSON यूआरएल ---
if (getActionBar() != null) { getActionBar().hide(); }

final android.media.MediaPlayer[] mp_container = new android.media.MediaPlayer[1];
final boolean[] isMusicEnabled = {true};
// अपने GitHub JSON का 'Raw' लिंक यहाँ डालें
final String GITHUB_JSON_URL = "https://raw.githubusercontent.com/आपका-यूसरनेम/आपका-रेपो/main/data.json";

mp_container[0] = android.media.MediaPlayer.create(this, getResources().getIdentifier("bg_tune", "raw", getPackageName()));
if (mp_container[0] != null) {
    mp_container[0].setLooping(true);
    mp_container[0].start();
}

// --- 2. मुख्य UI फ्रेमवर्क ---
final android.widget.FrameLayout main = new android.widget.FrameLayout(this);
main.setLayoutParams(new android.widget.FrameLayout.LayoutParams(-1, -1));

android.graphics.drawable.GradientDrawable gd = new android.graphics.drawable.GradientDrawable(
    android.graphics.drawable.GradientDrawable.Orientation.BR_TL,
    new int[] {Color.parseColor("#FDB99B"), Color.parseColor("#A770EF"), Color.parseColor("#FF0080")}
);
main.setBackground(gd);

// --- 3. हेडर और म्यूजिक टॉगल ---
final android.widget.LinearLayout header = new android.widget.LinearLayout(this);
header.setLayoutParams(new android.widget.FrameLayout.LayoutParams(-1, 145));
header.setGravity(android.view.Gravity.CENTER_VERTICAL);
header.setPadding(40, 0, 40, 0);
android.graphics.drawable.GradientDrawable h_gd = new android.graphics.drawable.GradientDrawable();
h_gd.setColor(Color.argb(130, 0, 0, 0)); 
h_gd.setCornerRadii(new float[]{0,0,0,0,55,55,55,55}); 
header.setBackground(h_gd);

final android.widget.TextView hTitle = new android.widget.TextView(this);
hTitle.setText("Yuva Kranti Brigade Barmer");
hTitle.setTextColor(Color.WHITE); hTitle.setTextSize(17); hTitle.setTypeface(null, android.graphics.Typeface.BOLD);
hTitle.setGravity(android.view.Gravity.CENTER);
android.widget.LinearLayout.LayoutParams titleLp = new android.widget.LinearLayout.LayoutParams(0, -2, 1.0f);
hTitle.setLayoutParams(titleLp);

final android.widget.TextView mToggle = new android.widget.TextView(this);
mToggle.setText("🪈"); mToggle.setTextSize(24);
mToggle.setOnClickListener(new android.view.View.OnClickListener() {
    @Override public void onClick(android.view.View _v) {
        if(isMusicEnabled[0]) { 
            if(mp_container[0] != null) mp_container[0].pause(); 
            mToggle.setText("🔇"); 
        } else { 
            if(mp_container[0] != null) mp_container[0].start(); 
            mToggle.setText("🪈"); 
        }
        isMusicEnabled[0] = !isMusicEnabled[0];
    }
});
header.addView(hTitle); header.addView(mToggle);

// --- 4. स्क्रॉल व्यू और कंटेंट ---
final android.widget.ScrollView sc = new android.widget.ScrollView(this);
sc.setLayoutParams(new android.widget.FrameLayout.LayoutParams(-1, -1));
sc.setVerticalScrollBarEnabled(false);
final android.widget.LinearLayout root = new android.widget.LinearLayout(this);
root.setOrientation(android.widget.LinearLayout.VERTICAL);
root.setPadding(40, 180, 40, 100); 
sc.addView(root);
main.addView(sc); main.addView(header);
setContentView(main);

// --- 5. लोगो और शपथ ---
final android.widget.ImageView logoView = new android.widget.ImageView(this);
android.widget.LinearLayout.LayoutParams l_lp = new android.widget.LinearLayout.LayoutParams(420, 420);
l_lp.gravity = android.view.Gravity.CENTER_HORIZONTAL;
l_lp.setMargins(0, 40, 0, 40);
logoView.setLayoutParams(l_lp);
try { logoView.setImageResource(getResources().getIdentifier("logo", "drawable", getPackageName())); } catch(Exception e){}
logoView.setOutlineProvider(new android.view.ViewOutlineProvider() {
    @Override public void getOutline(android.view.View v, android.graphics.Outline o) { o.setOval(0, 0, v.getWidth(), v.getHeight()); }
});
logoView.setClipToOutline(true);
root.addView(logoView);

android.widget.TextView sText = new android.widget.TextView(this);
sText.setText("\n“हम, बाड़मेर के जागरूक, जिम्मेदार और परिवर्तनकारी युवा, यह संकल्प लेते हैं कि समाज में व्याप्त भ्रष्टाचार, अन्याय, शोषण और अव्यवस्था के विरुद्ध संगठित होकर संघर्ष करेंगे।”\n");
sText.setTextSize(16); sText.setTextColor(Color.WHITE);
sText.setGravity(android.view.Gravity.CENTER);
sText.setTypeface(null, android.graphics.Typeface.ITALIC);
sText.setLineSpacing(8, 1.2f);
root.addView(sText);

// बटन फंक्शन्स
addFixedBtn(root, "📖 Constitution (संविधान)", 1); 
addSpace(root, 20);
addFixedBtn(root, "बदलाव के साथी बनें", 2);
addSpace(root, 80);

// --- 6. संस्थापक अनुभाग ---
final android.widget.LinearLayout fBox = new android.widget.LinearLayout(this);
fBox.setOrientation(android.widget.LinearLayout.VERTICAL);
fBox.setGravity(android.view.Gravity.CENTER); 
fBox.setPadding(40, 50, 40, 50);
android.widget.LinearLayout.LayoutParams f_lp = new android.widget.LinearLayout.LayoutParams(-1, -2);
f_lp.setMargins(0, 40, 0, 80);
fBox.setLayoutParams(f_lp);
android.graphics.drawable.GradientDrawable f_bg = new android.graphics.drawable.GradientDrawable();
f_bg.setColor(Color.argb(55, 255, 255, 255)); f_bg.setCornerRadius(60);
fBox.setBackground(f_bg);

final android.widget.ImageView fImg = new android.widget.ImageView(this);
fImg.setLayoutParams(new android.widget.LinearLayout.LayoutParams(250, 250));
fImg.setScaleType(android.widget.ImageView.ScaleType.CENTER_CROP);
try { fImg.setImageResource(getResources().getIdentifier("founder_photo", "drawable", getPackageName())); } catch(Exception e){}
fImg.setOutlineProvider(new android.view.ViewOutlineProvider() {
    @Override public void getOutline(android.view.View v, android.graphics.Outline o) { o.setOval(0, 0, v.getWidth(), v.getHeight()); }
});
fImg.setClipToOutline(true);
fBox.addView(fImg);

android.widget.TextView fName = new android.widget.TextView(this);
fName.setText("जितेंद्र सियोल \n(संस्थापक)");
fName.setTextSize(18); fName.setTextColor(Color.WHITE); fName.setTypeface(null, android.graphics.Typeface.BOLD);
fName.setGravity(android.view.Gravity.CENTER); 
fName.setPadding(0, 25, 0, 5);
fBox.addView(fName);

fBox.setOnClickListener(new android.view.View.OnClickListener() {
    @Override public void onClick(final android.view.View _v) {
        showCenteredMenu("Connect with Founder", "jitendersiyol", "channel/0029Va5NAqt6mYPQneu1uq0e", "@jitendrasiyol.1");
    }
});
root.addView(fBox);

// --- 7. सोशल मीडिया और कोट्स ---
addCenteredBar(root, "Instagram", "insta_logo", "https://www.instagram.com/yuvakrantibrigade");
addCenteredBar(root, "WhatsApp Group", "wa_logo", "https://chat.whatsapp.com/Gyx2hS9scOhLCMcrtJfgUU");

// --- 8. GitHub JSON और नोटिफिकेशन लॉजिक ---
new Thread(new Runnable() {
    @Override public void run() {
        try {
            java.net.URL url = new java.net.URL(GITHUB_JSON_URL);
            java.net.HttpURLConnection conn = (java.net.HttpURLConnection) url.openConnection();
            java.io.BufferedReader reader = new java.io.BufferedReader(new java.io.InputStreamReader(conn.getInputStream()));
            StringBuilder sb = new StringBuilder();
            String line;
            while ((line = reader.readLine()) != null) { sb.append(line); }
            final org.json.JSONObject json = new org.json.JSONObject(sb.toString());
            
            runOnUiThread(new Runnable() {
                @Override public void run() {
                    try {
                        String title = json.getString("title");
                        String msg = json.getString("message");
                        showPushNotification(title, msg);
                    } catch (Exception e) {}
                }
            });
        } catch (Exception e) {}
    }
}).start();

// --- 9. लाइफसाइकिल कंट्रोल ---
final android.app.Application.ActivityLifecycleCallbacks callbacks = new android.app.Application.ActivityLifecycleCallbacks() {
    @Override public void onActivityPaused(android.app.Activity a) {
        if (a == MainActivity.this && mp_container[0] != null && mp_container[0].isPlaying()) {
            mp_container[0].pause();
        }
    }
    @Override public void onActivityResumed(android.app.Activity a) {
        if (a == MainActivity.this && mp_container[0] != null && isMusicEnabled[0]) {
            mp_container[0].start();
        }
    }
    @Override public void onActivityDestroyed(android.app.Activity a) {
        if (a == MainActivity.this && mp_container[0] != null) {
            mp_container[0].release();
            mp_container[0] = null;
        }
    }
    @Override public void onActivityStopped(android.app.Activity a) {}
    @Override public void onActivitySaveInstanceState(android.app.Activity a, android.os.Bundle b) {}
    @Override public void onActivityCreated(android.app.Activity a, android.os.Bundle b) {}
    @Override public void onActivityStarted(android.app.Activity a) {}
};
getApplication().registerActivityLifecycleCallbacks(callbacks);

} // onCreate End

// --- हेल्पर्स और नोटिफिकेशन मेथड ---

private void showPushNotification(String title, String message) {
    android.app.NotificationManager nm = (android.app.NotificationManager) getSystemService(android.content.Context.NOTIFICATION_SERVICE);
    String channelId = "YKB_Updates";
    if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.O) {
        android.app.NotificationChannel channel = new android.app.NotificationChannel(channelId, "YKB News", android.app.NotificationManager.IMPORTANCE_HIGH);
        nm.createNotificationChannel(channel);
    }
    android.app.Notification.Builder builder = new android.app.Notification.Builder(this)
        .setSmallIcon(android.R.drawable.ic_dialog_info)
        .setContentTitle(title)
        .setContentText(message)
        .setAutoCancel(true);
    if (android.os.Build.VERSION.SDK_INT >= android.os.Build.VERSION_CODES.O) { builder.setChannelId(channelId); }
    nm.notify(1, builder.build());
}

private void openConstitutionText() {
    String txt = "";
    try {
        java.io.InputStream is = getAssets().open("constitution.txt");
        byte[] buffer = new byte[is.available()];
        is.read(buffer); is.close();
        txt = new String(buffer, "UTF-8");
    } catch (Exception e) { txt = "संविधान की फाइल लोड नहीं हो सकी।"; }
    android.widget.ScrollView sv = new android.widget.ScrollView(this);
    android.widget.TextView tv = new android.widget.TextView(this);
    tv.setText(txt); tv.setPadding(50, 50, 50, 50); tv.setTextColor(Color.BLACK);
    sv.addView(tv);
    new android.app.AlertDialog.Builder(this).setTitle("भारतीय संविधान").setView(sv).setPositiveButton("ठीक है", null).show();
}

private void addFixedBtn(android.widget.LinearLayout r, String t, final int type) {
    android.widget.LinearLayout l = new android.widget.LinearLayout(this);
    l.setLayoutParams(new android.widget.LinearLayout.LayoutParams(-1, dp(60)));
    l.setGravity(android.view.Gravity.CENTER);
    android.graphics.drawable.GradientDrawable s = new android.graphics.drawable.GradientDrawable();
    s.setColor(Color.WHITE); s.setCornerRadius(dp(30));
    l.setBackground(new android.graphics.drawable.RippleDrawable(android.content.res.ColorStateList.valueOf(Color.parseColor("#E19DD2")), s, null));
    android.widget.TextView tv = new android.widget.TextView(this);
    tv.setText(t); tv.setTextColor(Color.BLACK);
    l.addView(tv); 
    l.setOnClickListener(new android.view.View.OnClickListener() {
        @Override public void onClick(android.view.View v) {
            if (type == 1) openConstitutionText();
            else startActivity(new android.content.Intent(android.content.Intent.ACTION_VIEW, android.net.Uri.parse("https://forms.zohopublic.in/yuvakrantibrigadegm1/form/YuvaKrantiBrigadejoin/formperma/rRohSDbZ9FomO5V_xbX2ZipY_VMMVidO7uWDdHMS254")));
        }
    });
    r.addView(l);
}

private void showCenteredMenu(String title, final String i, final String w, final String y) {
    android.widget.LinearLayout l = new android.widget.LinearLayout(this);
    l.setOrientation(android.widget.LinearLayout.VERTICAL);
    l.setPadding(30, 30, 30, 30); l.setGravity(android.view.Gravity.CENTER);
    addOption(l, "Instagram", "insta_logo", "https://www.instagram.com/" + i);
    addOption(l, "WhatsApp", "wa_logo", "https://whatsapp.com/" + w);
    new android.app.AlertDialog.Builder(this).setTitle(title).setView(l).setPositiveButton("बंद करें", null).show();
}

private void addOption(android.widget.LinearLayout p, String n, String ic, final String u) {
    android.widget.LinearLayout i = new android.widget.LinearLayout(this);
    i.setGravity(android.view.Gravity.CENTER); i.setPadding(20, 30, 20, 30);
    android.widget.TextView tv = new android.widget.TextView(this);
    tv.setText(n); tv.setTextColor(Color.BLACK);
    i.addView(tv);
    i.setOnClickListener(new android.view.View.OnClickListener() {
        @Override public void onClick(android.view.View v) { startActivity(new android.content.Intent(android.content.Intent.ACTION_VIEW, android.net.Uri.parse(u))); }
    });
    p.addView(i);
}

private void addCenteredBar(android.widget.LinearLayout r, String t, String img, final String u) {
    android.widget.LinearLayout l = new android.widget.LinearLayout(this);
    l.setGravity(android.view.Gravity.CENTER);
    android.widget.LinearLayout.LayoutParams lp = new android.widget.LinearLayout.LayoutParams(-1, dp(60));
    lp.setMargins(0, 15, 0, 15); l.setLayoutParams(lp);
    android.graphics.drawable.GradientDrawable s = new android.graphics.drawable.GradientDrawable();
    s.setColor(Color.WHITE); s.setCornerRadius(dp(30));
    l.setBackground(s);
    android.widget.TextView tv = new android.widget.TextView(this);
    tv.setText(t); tv.setTextColor(Color.BLACK);
    l.addView(tv);
    l.setOnClickListener(new android.view.View.OnClickListener() {
        @Override public void onClick(android.view.View v) { startActivity(new android.content.Intent(android.content.Intent.ACTION_VIEW, android.net.Uri.parse(u))); }
    });
    r.addView(l);
}

private int dp(int d) { return (int) (d * getResources().getDisplayMetrics().density + 0.5f); }

private void addSpace(android.widget.LinearLayout r, int h) {
    android.view.View s = new android.view.View(this); s.setLayoutParams(new android.widget.LinearLayout.LayoutParams(-1, dp(h))); r.addView(s);
}

{ // क्लोजिंग
# Yuvaofbmr
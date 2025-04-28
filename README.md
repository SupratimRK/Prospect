# Prospect Chat - Where Electrons Meet Emojis 💬⚡️

**(Crafted by Supratim - Yesss! That's mee!)**

---

## 🧐 Whatcha Lookin' At? Prospect Chat!

Alright, listen up, code comrades and chat champs! 👋 Ever thought, "Man, I wish I could build my *own* chat app?" Well, **SupratimRK** did. He's an Electronics Engineer who apparently got bored of just making hardware do his bidding and decided to boss around some PHP too. The result? **Prospect Chat!**

This ain't just another chat app. It's a testament to caffeine, curiosity, and the sheer audacity of an EC guy diving headfirst into web dev. Built with a cocktail of **PHP**, **MySQL**, **HTML/CSS**, and a dash of **JavaScript** wizardry, Prospect Chat lets you sign up, log in, and gossip with your pals in real-time. No carrier pigeons needed. 🕊️

So, whether you're here to learn, contribute, or just silently judge Supratim's PHP skills (kidding... mostly 😉), welcome aboard!

---

## 🔥 Features - What's Cookin'?

This chat app might look simple, but it's got some nifty tricks up its sleeve:

*   **Signup & Login Like a Boss**:
    *   Jump in fresh! Sign up with your deets and a killer profile pic (stored safely in `php/images/`, btw).
    *   Already part of the cool club? Log in securely. We don't peek at your passwords (promise!). Handled by `index.php`, `login.php`, `php/signup.php`, and `php/login.php`.
*   **Real-Time Banter**:
    *   Messages pop up faster than you can say "Did you try turning it off and on again?". Thanks to JavaScript (`javascript/chat.js`) and PHP (`php/insert-chat.php`, `php/get-chat.php`) working together like best buds.
*   **Know Who's Lurking (User Status)**:
    *   See if your friends are "Active now" or "Offline" (probably snacking). Updates when you log in/out (`php/login.php`, `php/logout.php`).
*   **Looks Good Everywhere (Responsive Design)**:
    *   Chat from your giant monitor or your tiny phone screen. It just *works*. Magic, right? (Okay, it's CSS - `style.css`).
*   **Profile Pics**:
    *   Because who wants to chat with a boring default icon? Show off that smile!

---

## 🚀 Get It Running - DIY Time!

Feeling brave? Wanna host this bad boy yourself? Let's get our hands dirty!

### 1. Grab the Code (Clone Wars!)
First, you gotta snag the code. Open your terminal and channel your inner hacker:
```bash
git clone https://github.com/SupratimRK/Prospect.git
cd Prospect
```

### 2. Database Drama
Time to set up the brain of the operation – the MySQL database:

*   Whip open your favorite MySQL tool (phpMyAdmin, MySQL Workbench, or just the command line if you're hardcore).
*   Create a new database. Let's call it `chatapp` (or whatever floats your boat).
*   Import the included `chatapp.sql` file. This sets up the `users` and `messages` tables.
    ```bash
    # If you're using the command line:
    mysql -u your_mysql_username -p chatapp < chatapp.sql
    ```
*   *Voila!* Database ready for gossip.

### 3. Tell PHP Where the Party's At (Configuration)
PHP needs to know how to talk to your database. Edit the `php/config.php` file with your MySQL username, password, and database name:

```php
<?php
  // Yo PHP, connect to this database, alright?
  $hostname = "localhost"; // Usually localhost, unless you're fancy
  $username = "your_mysql_username"; // Your MySQL username
  $password = "your_mysql_password"; // Your MySQL password (shhh!)
  $dbname = "chatapp"; // The database name you created

  $conn = mysqli_connect($hostname, $username, $password, $dbname);
  if(!$conn){
    // If it breaks, complain loudly!
    echo "Database connection error".mysqli_connect_error();
  }
?>
```

### 4. Spin Up a Server
PHP files don't run themselves (sadly). You need a web server like Apache or Nginx with PHP support.
*   **Easy Mode:** Use tools like **XAMPP**, **WAMP**, or **MAMP**. Just drop the entire `Prospect` folder into the main web directory (like `htdocs` for XAMPP/MAMP, or `www` for WAMP).
*   **Manual Mode:** Configure your own Apache/Nginx server to point to the `Prospect` directory.

### 5. Browser Time!
Open your web browser and navigate to where you put the files. If you used XAMPP/WAMP/MAMP, it's probably:
```
http://localhost/Prospect/
```
If everything went right, you should see the Prospect Chat login/signup page. High five! 🙌

---

## 🛠️ Under the Hood - How the Magic Happens (Sort Of)

Curious how this contraption works? Here's the lowdown:

*   **Frontend Fun:** `index.php` (Signup), `login.php`, `chat.php`, and `users.php` provide the user interface you see and interact with. `style.css` makes it pretty. `header.php` is included on multiple pages for consistency. `logo.png` is... well, the logo!
*   **JavaScript Jazz:** The `javascript/` folder is where the client-side action is.
    *   `signup.js` & `login.js`: Handle form submissions without full page reloads (AJAX!).
    *   `users.js`: Probably fetches and displays the user list, maybe handles search?
    *   `chat.js`: The star player! Sends your messages, fetches new ones periodically using AJAX, and scrolls the chat window.
    *   `pass-show-hide.js`: Lets you peek at your password. Sneaky!
*   **PHP Powerhouse:** The `php/` directory is the backend brain.
    *   `config.php`: Database connection details (the secret sauce).
    *   `signup.php` & `php/login.php`: Handle user registration and login logic, session management, and password hashing (hopefully!). Handles image uploads to `php/images/`.
    *   `insert-chat.php`: Takes messages sent from `chat.js` and saves them to the database.
    *   `get-chat.php`: Fetches message history for the selected chat.
    *   `data.php`: Might be used to format user data for the user list or chat display.
    *   `users.php`: Provides data for the user list, likely fetched by `users.js`.
    *   `search.php`: Powers the user search bar.
    *   `logout.php`: Ends the user session and updates their status to "Offline".
*   **Database:** MySQL stores user info (`users` table) and chat messages (`messages` table) persistently, thanks to `chatapp.sql`.

---

## 📂 Project Structure - A Messy Desk Tour

Here’s a map of the important bits:

```
Prospect/
├── chat.php           # Main chat screen where the magic happens
├── chatapp.sql        # The blueprint for your database tables
├── header.php         # Probably a reusable header for pages?
├── index.php          # Signup page - Welcome, newbie!
├── javascript/        # Client-side brains (making things dynamic)
│   ├── chat.js        # Real-time message handling
│   ├── login.js       # Login form helper
│   ├── pass-show-hide.js # Password visibility toggle
│   ├── signup.js      # Signup form helper
│   └── users.js       # User list handling & search
├── login.php          # Login page - Welcome back!
├── logo.png           # The app's fancy logo
├── php/               # Server-side heavy lifting (the backend engine)
│   ├── config.php     # Database connection settings (IMPORTANT!)
│   ├── data.php       # Helper for formatting data?
│   ├── get-chat.php   # Fetches messages
│   ├── images/        # Where user profile pictures live! 🖼️
│   ├── insert-chat.php # Stores new messages
│   ├── login.php      # Login logic
│   ├── logout.php     # Logout logic & status update
│   ├── search.php     # User search logic
│   ├── signup.php     # Signup logic & image upload
│   └── users.php      # Fetches user list data
├── style.css          # Makes everything look snazzy ✨
├── unzipper.php       # A mysterious utility script... 🕵️
└── users.php          # Page to display the list of users
```
---

## 🖼️ Show Me the Pixels! (Screenshots)

*(I think, 🤔 I should totally add some screenshots here. Show off my creation! Login page, the chat interface... Just to make people jealous! 😎)*

---

## 🙌 Wanna Help? Contributing

Think you can make Prospect Chat even *more* awesome? Or maybe you found a bug? (Nooo, not possible! 😉) Contributions are welcome!

1.  **Fork** this repo (click the button top-right).
2.  Create a **new branch** for your amazing feature: `git checkout -b my-cool-new-feature`
3.  Code like the wind! Make your changes. Test them (pretty please?).
4.  **Commit** your changes: `git commit -m 'Added this super cool feature'`
5.  **Push** to your branch: `git push origin my-cool-new-feature`
6.  Open a **Pull Request** back to the main `Prospect` repo.

 I'll gaze upon your work, maybe ask a question or two, and if it's cool, merge it in! You'll be famous! (Well, GitHub-famous, anyway).

---

## 🤝 Big Thanks & High Fives!

Massive thanks for checking out Prospect Chat! Whether you're a seasoned dev, a curious student, or just someone who stumbled here, your interest means a lot. Hope you have fun with it! Keep coding, keep chatting, and maybe don't mix up your soldering iron with your keyboard. 😉

---

*Built with late nights, instant noodles, and a questionable amount of Chai ☕ by EC Engineer, [SupratimRK](https://github.com/SupratimRK). with log<sub>10</sub>(1) Social Life*

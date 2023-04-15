Juice Shop is a web application developed by OWASP (Open Web Application Security Project) that aims to raise awareness about web application security by presenting a vulnerable application.

The purpose of auditing Juice Shop is to detect security vulnerabilities in the application and recommend measures to fix those vulnerabilities. The audit can be performed by security auditors, penetration testers, or developers.


# Step 1: Running OWASP Juice Shop

## From sources

   1. Install Node.js on your computer.
   2. On the command line run `git clone https://github.com/juice-shop/juice-shop.git --depth 1`.
   3. Go into the cloned folder with `cd juice-shop`.
   4. Run `npm install`. This only has to be done before the first start or after you changed the source code.
   5. Run `npm start` to launch the application.
   6. Browse to `http://localhost:3000`.

## From pre-packaged distribution

   1. Install a 64bit Node.js on your Windows, MacOS or Linux machine.
   2. Download   juice-shop-<version>_<node-version>_<os>_x64.zip   (or .tgz) attached to the latest release on GitHub.
   3. Unpack the archive and run npm start in unpacked folder to launch the application
   4. Browse to `http://localhost:3000`.


## Docker image

You need to have Docker installed to run Juice Shop as a container inside it. Following the instructions below will download the current stable version (built from master branch on GitHub) which internally runs the application on the currently recommended Node.js version 18.x.



1. Install Docker on your computer.
2. On the command line run `docker pull bkimminich/juice-shop` to download the latest image described above.
3. Run `docker run -d -p 3000:3000 bkimminich/juice-shop` to launch the container with that image.
4. Browse to `http://localhost:3000`.

If you are using Docker on Windows - inside a VirtualBox VM - make sure that you also enable port forwarding from host 127.0.0.1:3000 to 0.0.0.0:3000 for TCP.



# Step 2: Challenge tracking
## The Score Board

In order to motivate you to hunt for vulnerabilities, it makes sense to give you at least an idea what challenges are available in the application. Also, you should know when you actually solved a challenge successfully, so you can move on to another task. Both these cases are covered by the application's score board.

On the score board you can view a list of all available challenges with a brief description. Some descriptions are very explicit hacking instructions. Others are just vague hints that leave it up to you to find out what needs to be done.

Partly solved Score Board
![score-board_partly](https://user-images.githubusercontent.com/91556798/232218571-0e539f51-3aff-40ba-a82b-55c34c696d63.png)

The challenges are rated with a difficulty level between ⭐ and ⭐⭐⭐⭐⭐⭐, with more stars representing a higher difficulty. To make the list of challenges less daunting, they are clustered by difficulty. By default, only the 1-star challenges are unfolded. You can open or collapse all challenge blocks as you like. Collapsing a block has no impact on whether you can solve any of its challenges.

The difficulty ratings have been continually adjusted over time based on user feedback. The ratings allow you to manage your own hacking pace and learning curve significantly. When you pick a 5- or 6-star challenge you should expect a real challenge and should be less frustrated if you fail on it several times. On the other hand if hacking a 1- or 2-star challenge takes very long, you might realize quickly that you are on a wrong track with your chosen hacking approach.

Finally, each challenge states if it is currently unsolved or solved. The current overall progress is represented in a progress bar on top of the score board. Especially in group hacking sessions this allows for a bit of competition between the participants.



Success notifications.

The OWASP Juice Shop employs a simple yet powerful gamification mechanism: Instant success feedback! Whenever you solve a hacking challenge, a notification is immediately shown on the user interface.

![challenge_solved_notification](https://user-images.githubusercontent.com/91556798/232219561-de6ab7b4-dc9d-4062-abd7-9e1cc45a6d7d.png)

"Challenge solved!" push notification

This feature makes it unnecessary to switch back and forth between the screen you are attacking, and the score board to verify if you succeeded. Some challenges will force you to perform an attack outside of the Juice Shop web interface, e.g. by interacting with the REST API directly. In these cases the success notification will light up when you come back to the regular web UI the next time.

To make sure you do not miss any notifications they do not disappear automatically after a timeout. You have to dismiss them explicitly. In case a number of notifications "piled up" it is not necessary to dismiss each one individually, as you can simply Shift-click one of their X-buttons to dismiss all at the same time.

Depending on your application configuration, each challenge notification might also show a 🏁 symbol with a character sequence next to it. If you are doing a hacking session just on your own, you can completely ignore this flag. The code is only relevant if you are participating in a CTF event.

![notification_with_flag](https://user-images.githubusercontent.com/91556798/232219792-430b76ed-f7c9-454a-b4a4-1aab6bc5ec45.png)

Automatic saving and restoring hacking progress:

The self-healing feature - by wiping the entire database on server start - of Juice Shop was advertised as a benefit just a few pages before. This feature comes at a cost, though: As the challenges are also part of the database schema, they will be wiped along with all the other data. This means, that after every restart you start with a clean 0% score board and all challenges in unsolved state.

To keep the resilience against data corruption but allow users to pick up where they left off after a server restart, your hacking progress is automatically saved whenever you solve a challenge - as long as you allow Browser cookies!

After restarting the server, once you visit the application your hacking progress is automatically restored:

![autorestore-hacking-progress](https://user-images.githubusercontent.com/91556798/232227338-1d1b6e8f-9283-4f72-8ab4-e9b583e7d13f.png)

The auto-save mechanism keeps your progress for up to 30 days after your previous hacking session. When the score board is restored to its prior state, a torrent of success notifications will light up - depending on how many challenges you solved up to that point. As mentioned earlier these can be bulk-dismissed by Shift-clicking any of the X-buttons.

If you want to start over with a fresh hacking session, simply click the Delete cookie to clear hacking progress button. After the next server restart, your score board will be blank.
Manual progress and settings backup

With the round Backup and Restore buttons on the Score Board you can save and later restore your hacking progress as well as language, Score Board filters, banner dismissal to a JSON file.

![manual_backup](https://user-images.githubusercontent.com/91556798/232227373-aa7384bd-89a3-4e53-a85a-37649a134ea8.png)

The backup format is independent of your system or browser, meaning you can use the backup file to conveniently transfer your progress and settings from one computer to another. Example:

```
{
  "version": 1,
  "scoreBoard": {
    "displayedDifficulties": [ 1, 2, 3 ],
    "displayedChallengeCategories": [
      "Broken Access Control",
      "Broken Anti Automation"
    ]
  },
  "banners": {
    "welcomeBannerStatus": "dismiss",
    "cookieConsentStatus": "dismiss"
  },
  "language": "de_DE",
  "continueCode": "rzJBXpa...bm45J2okY7LX4v7o"
}
```




When the backup restore is successful, you must click "Apply changes now" in the corresponding message to trigger the hacking progress restore as well as the language changes in backend data.


![manual_backup-restore](https://user-images.githubusercontent.com/91556798/232227435-c3a12733-eefd-4ba6-b36c-ad1f040fea24.png)

If you do not click that button before the message vanishes, you can also restart your application server to apply the backup of hacking progress.

If during restore you see an error message Version X is incompatible with expected version Y your backup was taken before a semantically incompatible format change.


# Step 3: Hacking Instructor:

The built-in Hacking Instructor offers tutorials for some Juice Shop challenges. By default, the welcome banner shown upon first launch of the application has a mortar_board-button which will help you Find the carefully hidden 'Score Board' page.

![welcome-banner](https://user-images.githubusercontent.com/91556798/232227705-d9d26922-c681-48f6-9f13-7bbb0a867682.png)

On the Score Board itself you will then find similar mortar_board-buttons on some challenges which will launch a corresponding tutorial for each as well. All tutorials consist of a scripted sequence of helpful hints and instructions.

![hacking-instructor_1](https://user-images.githubusercontent.com/91556798/232227728-19240c52-2661-485b-ac20-c3b0383c2210.png)

The scripts often provide some interaction, like waiting for the user to make some specific input or having them visit another dialog before continuing. Some hints or instructions can be skipped by just clicking on them.

![hacking-instructor_2](https://user-images.githubusercontent.com/91556798/232227756-9268e612-8e0c-4448-a9e4-cbd613237df0.png)


After successfully completing all steps of a tutorial, the Hacking Instructor will usually congratulate you and then go into hiding until summoned again for another hacking challenge via the Score Board.

![hacking-instructor_3](https://user-images.githubusercontent.com/91556798/232233581-b23d2637-603f-47bb-99d0-809deb47a4fd.png)

# Step 4: Coding challenges

For many (solved) challenges an additional button is available on the Score Board which
will open a dialog containing the actual code snippet responsible for the security vulnerability behind the particular challenge. Note that by default this button is only enabled for solved hacking challenges. For challenge where no such button is shown, there is no coding challenge available.

![code_snippet1](https://user-images.githubusercontent.com/91556798/232233791-b83c703e-1a59-4d36-acd8-2638b3883285.png)

This snippet is loaded in real-time from the running application's actual code base and is sanitized to not show any "challenge check" or similar code that would not be present in a real-world application.

![code_snippet2](https://user-images.githubusercontent.com/91556798/232233810-e4d94b5e-a20a-44a3-87fc-1d6bad0d4724.png)

The user can try to identify the actual line(s) of code responsible for the vulnerability behind the particular challenge. When they submit their selection, the server will provide feedback on the choice.

![code_snippet3](https://user-images.githubusercontent.com/91556798/232233842-9a2dfcc7-5701-4522-a518-d959c4316576.png)

If the correct line(s) were submitted, the user will be presented with 3-4 possible options to fix the vulnerability. They can use the built-in code comparison to view them and then make a selection of what they think to be the correct fix. Submitting their choice to the server will again lead to feedback.

![code_snippet4](https://user-images.githubusercontent.com/91556798/232233863-18c3c61a-2318-4656-a45d-6e8ad9db7182.png)

The progress with coding challenges is not factored into the percentage bar at the top of the Score Board. For each coding challenge the current status is represented by the button to launch it. Once the "Find It" and "Fix It" part are solved, the button turns green. While only the "Find It" part was solved, a small green "1/2"-badge indicates having made it half-way.

![code_snippet5](https://user-images.githubusercontent.com/91556798/232233892-722c2a06-6efc-4491-96f3-b2e3ff86be12.png)

When either of the two steps is solved correctly, the confetti cannons fire both barrels to celebrate the user's success.

![confetti2](https://user-images.githubusercontent.com/91556798/232233922-6f276f0a-2b83-43b0-ae86-4dc3cddf9155.png)

# Potentially dangerous challenges

![mitigation_links](https://user-images.githubusercontent.com/91556798/232234018-87b83129-5cb5-4776-b038-76d9f2bf9b5c.png)

Some challenges can cause potential harm or pose some danger for your computer, i.e. the XXE, SSTi and Deserialization challenges as well as two of the NoSQLi challenges, and the possibility of an arbitrary file write. These simply cannot be sandboxed in a 100% secure way. These are only dangerous if you use actually malicious payloads, so please do not play with payloads you do not fully understand. Furthermore, be aware all stored XSS vulnerabilities can - by their nature - be abused to perform harmful attacks on unsuspecting visitors.

For safety reasons all potentially dangerous challenges are disabled (along with their underlying vulnerabilities) when a containerized environment is detected. By default, this applies to Docker, Heroku, and Gitpod. Dangerous challenges are marked as 'unavailable' in the scoreboard as can be seen in the screenshot above.

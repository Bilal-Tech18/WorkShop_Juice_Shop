Juice Shop is a web application developed by OWASP (Open Web Application Security Project) that aims to raise awareness about web application security by presenting a vulnerable application.

The purpose of auditing Juice Shop is to detect security vulnerabilities in the application and recommend measures to fix those vulnerabilities. The audit can be performed by security auditors, penetration testers, or developers.


Running OWASP Juice Shop

From sources

   1. Install Node.js on your computer.
   2. On the command line run  git clone https://github.com/juice-shop/juice-shop.git --depth 1 .
   3. Go into the cloned folder with cd juice-shop
   4. Run npm install. This only has to be done before the first start or after you changed the source code.
   5. Run npm start to launch the application.
   6. Browse to http://localhost:3000

From pre-packaged distribution

    Install a 64bit Node.js on your Windows, MacOS or Linux machine.
    Download   juice-shop-<version>_<node-version>_<os>_x64.zip   (or .tgz) attached to the latest release on GitHub.
    Unpack the archive and run npm start in unpacked folder to launch the application
    Browse to http://localhost:3000


Docker image

You need to have Docker installed to run Juice Shop as a container inside it. Following the instructions below will download the current stable version (built from master branch on GitHub) which internally runs the application on the currently recommended Node.js version 18.x.

    Install Docker on your computer.
    On the command line run docker pull bkimminich/juice-shop to download the latest image described above.
    Run docker run -d -p 3000:3000 bkimminich/juice-shop to launch the container with that image.
    Browse to http://localhost:3000.

If you are using Docker on Windows - inside a VirtualBox VM - make sure that you also enable port forwarding from host 127.0.0.1:3000 to 0.0.0.0:3000 for TCP.



Challenge tracking
The Score Board

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

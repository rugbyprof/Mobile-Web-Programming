## Project: Where In The World Is Tyler Hackbarth?!?

### Part 1: Creating our backend (server side)
#### Due: Monday Aug 4th by 1:00 p.m.

-----

### Overview

This is going to be an app that allows the members of the class to find / locate other members of the class, especially those who skip class. This app will show a set of icons on a google map, where each icon depicts the location of class member. 

### 1 - Create Workspace

- Create a folder in: `/var/www/html/` called `Program2A`
- Change into your `Program2A` folder.
- Run the following commands:

```bash
wget https://gist.githubusercontent.com/rugbyprof/5ee5f9c7b72fe87d571e/raw/905b7ea4d03abc21b8d12bfa69d6aef08a5825d7/index.html
wget https://gist.githubusercontent.com/rugbyprof/60eb31d32be47f9d6531/raw/0215193c8850750e084bd3989d653dc3bdda2e2b/simple-sidebar.css
wget https://gist.githubusercontent.com/rugbyprof/0092fe67293fac2be65c/raw/79332abcdb32ca9beac1be09a337d96ebce0aea9/backend.php
wget https://gist.githubusercontent.com/rugbyprof/54f43596aee4432fe959/raw/18f3c0166ea804569368a75dbb88772eaf25ddaf/geo.js
```

Those commands grab these gists:
- [index.html](https://gist.github.com/rugbyprof/5ee5f9c7b72fe87d571e)
- [simple-sidebar.css](https://gist.github.com/rugbyprof/60eb31d32be47f9d6531)
- [backend.php](https://gist.github.com/rugbyprof/0092fe67293fac2be65c)
- [geo.js](https://gist.github.com/rugbyprof/54f43596aee4432fe959)

Now create these files in your folder:
- `signup.html`
- `login.html`

When completed you should have a folder that contains:
- ![1] Program2A
    - ![2] backend.php
    - ![2] index.html
    - ![2] geo.js
    - ![2] login.html
    - ![2] signup.html
    - ![2] simple-sidebar.css

-----

### 2 Create A New Database & A New Database User

- Log into phpmyadmin on your server.
- Create a new database called `mobile_web`.
- Create a new user called `mobile` with a password of `33r9ghijk`.

- Click <br>
> ![](http://f.cl.ly/items/01013M0q3I3B2M122W1a/Screen%20Shot%202014-07-24%20at%208.30.11%20PM.png)

- Then Click <br>
> ![](http://f.cl.ly/items/0L2B352D401E2Y0d1p1S/add_user_small.png)

- This brings up a form:<br>
>![](http://f.cl.ly/items/1U060j2r3m04270t3R20/form_small.png)<br>
Notice the `red arrow`, it's pointing to a checkbox that, when checked, will grant all priveleges to a user that has the same root name as a database. So our user `mobile` will get all priveleges on database `mobile_web`.

-----

### 3 Create & Populate Database Tables 

- Select the `mobile_web` database from the side bar
- Then click on the `SQL` button:<br>![](http://f.cl.ly/items/1c2o0f0Q362G3N1p1p1D/sql_button_small.png) 
- Then paste in the following `SQL` code.<br>

```sql
CREATE TABLE IF NOT EXISTS `Users` (
  `Id` int(8) NOT NULL,
  `First` varchar(32) NOT NULL,
  `Last` varchar(32) NOT NULL,
  `Thumbnail` varchar(128) NOT NULL,
  `Lat` float(11,7) NOT NULL,
  `Lon` float(11,7) NOT NULL,
  `Sex` enum('M','F') NOT NULL,
  `Phone` varchar(14) NOT NULL,
  `Email` varchar(128) NOT NULL,
  `Busy` tinyint(1) NOT NULL,
  `LoggedIn` tinyint(1) NOT NULL,
  `Password` varchar(64) NOT NULL,
  PRIMARY KEY (`Id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;


INSERT INTO `Users` (`Id`, `First`, `Last`, `Thumbnail`, `Lat`, `Lon`, `Sex`, `Phone`, `Email`, `Busy`, `LoggedIn`, `Password`) VALUES
(1, 'Brian', 'Harper', 'http://api.randomuser.me/portraits/men/80.jpg', 0.0000000, 0.0000000, 'M', '(190)-480-4137', 'brian.harper66@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(2, 'Troy', 'Anderson', 'http://api.randomuser.me/portraits/men/25.jpg', 0.0000000, 0.0000000, 'M', '(798)-131-8886', 'troy.anderson59@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(3, 'Terry', 'Pierce', 'http://api.randomuser.me/portraits/men/46.jpg', 0.0000000, 0.0000000, 'M', '(612)-523-5742', 'terry.pierce20@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(4, 'Georgia', 'Lawrence', 'http://api.randomuser.me/portraits/women/28.jpg', 0.0000000, 0.0000000, 'F', '(298)-191-3008', 'georgia.lawrence62@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(5, 'Annie', 'Bishop', 'http://api.randomuser.me/portraits/women/91.jpg', 0.0000000, 0.0000000, 'F', '(192)-605-8261', 'annie.bishop87@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(6, 'Tonya', 'Bradley', 'http://api.randomuser.me/portraits/women/4.jpg', 0.0000000, 0.0000000, 'F', '(935)-761-3589', 'tonya.bradley88@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(7, 'Juan', 'Fox', 'http://api.randomuser.me/portraits/men/30.jpg', 0.0000000, 0.0000000, 'M', '(468)-137-9655', 'juan.fox81@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(8, 'Teresa', 'Fields', 'http://api.randomuser.me/portraits/women/92.jpg', 0.0000000, 0.0000000, 'F', '(639)-679-9466', 'teresa.fields78@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(9, 'Randall', 'Carpenter', 'http://api.randomuser.me/portraits/men/37.jpg', 0.0000000, 0.0000000, 'M', '(673)-641-8672', 'randall.carpenter98@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(10, 'Bobbie', 'Smith', 'http://api.randomuser.me/portraits/women/68.jpg', 0.0000000, 0.0000000, 'F', '(440)-696-8216', 'bobbie.smith25@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(11, 'Taylor', 'Curtis', 'http://api.randomuser.me/portraits/women/67.jpg', 0.0000000, 0.0000000, 'F', '(149)-948-7170', 'taylor.curtis36@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(12, 'Karl', 'Meyer', 'http://api.randomuser.me/portraits/men/2.jpg', 0.0000000, 0.0000000, 'M', '(187)-405-6885', 'karl.meyer98@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(13, 'Stacy', 'Willis', 'http://api.randomuser.me/portraits/women/91.jpg', 0.0000000, 0.0000000, 'F', '(955)-545-2350', 'stacy.willis54@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(14, 'Kurt', 'Chapman', 'http://api.randomuser.me/portraits/men/28.jpg', 0.0000000, 0.0000000, 'M', '(880)-318-6738', 'kurt.chapman37@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(15, 'Dolores', 'Welch', 'http://api.randomuser.me/portraits/women/74.jpg', 0.0000000, 0.0000000, 'F', '(432)-439-5317', 'dolores.welch95@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(16, 'Carrie', 'Gonzalez', 'http://api.randomuser.me/portraits/women/75.jpg', 0.0000000, 0.0000000, 'F', '(829)-315-9981', 'carrie.gonzalez28@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(17, 'Chester', 'Sullivan', 'http://api.randomuser.me/portraits/men/71.jpg', 0.0000000, 0.0000000, 'M', '(132)-614-7874', 'chester.sullivan87@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(18, 'Dana', 'Phillips', 'http://api.randomuser.me/portraits/women/15.jpg', 0.0000000, 0.0000000, 'F', '(383)-282-6694', 'dana.phillips50@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(19, 'Layla', 'Holmes', 'http://api.randomuser.me/portraits/women/88.jpg', 0.0000000, 0.0000000, 'F', '(844)-930-3814', 'layla.holmes46@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99'),
(20, 'Henry', 'Oliver', 'http://api.randomuser.me/portraits/men/44.jpg', 0.0000000, 0.0000000, 'M', '(556)-611-8198', 'henry.oliver94@example.com', 0, 0, '5f4dcc3b5aa765d61d8327deb882cf99');

CREATE TABLE IF NOT EXISTS `Users_History` (
  `Id` int(8) NOT NULL,
  `Lat` float(11,7) NOT NULL,
  `Lon` float(11,7) NOT NULL,
  `GeoEncodedAddress` text NOT NULL,
  `StopLabel` varchar(64) NOT NULL,
  `StopType` varchar(64) NOT NULL,
  `time_stamp` int(15) NOT NULL,
  PRIMARY KEY (`Id`)
) ENGINE=InnoDB DEFAULT CHARSET=latin1;
```

-----


[1]: https://cdn1.iconfinder.com/data/icons/UltimateGnome/22x22/status/folder-drag-accept.png "Folder"
[2]: http://www.plcs.net/downloads/images/defaut.gif "File"

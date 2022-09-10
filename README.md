<p align="center">
  <img src="https://pbs.twimg.com/media/FNRJpPdXsAAbSQu?format=png&name=small">
</p>

# Project: "Add an Offline Mode in [OpenFoodFacts Mobile App](https://github.com/openfoodfacts/smooth-app)"

| **Student**      | Aman Raj                                                                                                                                         |
| :--------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Organisation** | [Open Food Facts](https://world.openfoodfacts.org/)                                                                                              |
| **Project**      | [Implement an offline mode for the new Open Food Facts Flutter application](https://summerofcode.withgoogle.com/programs/2022/projects/0B0YhUb3) |
| **GitHub**       | [@ashaman999](https://github.com/ashaman999)                                                                                                     |
| **LinkedIn**     | [Aman Raj](https://www.linkedin.com/in/ashaman999/)                                                                                              |
| **Email**        | <a href="mailto:amanpie@gmail.com">amanpie@gmail.com</a>                                                                                         |
| **Website**      | [https://ashaman999.github.io/ashaman/](https://ashaman999.github.io/ashaman/)                                                                   |

# About Me

Hello, I am Aman Raj, I am in my pre-final year the time when I am doing my GSoC, I am from Bihar India. I started contributing to open food facts a while ago, for issues regarding the features I did during my GSoC period, feel free to reach me through my Email or on LinkedIn

# Special thanks to my mentor and community:

- Edouard Marquez [@Github](https://github.com/g123k) [@LinkedIn](https://www.linkedin.com/in/edouard-marquez-32431514/)
- Marvin Möltgen [@Github](https://github.com/M123-dev) [@LinkedIn](https://www.linkedin.com/in/marvin-m%C3%B6ltgen-9504391a7/)

##### Also Big Thanks to Project Maintainers for helping with organizing things nicely

- Pierre Slamich [@Github](https://github.com/teolemon) [@LinkedIn](https://www.linkedin.com/in/pierreslamich/)

# Primary Goals of the Project

- Implementing the Offline Product Save Mechanism
- Offline Edit Mode (Let user modify changes and sync with server when back online)
- Preloading data (Let users load the top 1000 scanned products within their country)

The main goal was somewhat already implemented, my work was mostly to retune the existing way to have a better experience for end users. I did the way to store gzipped data instead of raw JSON to further reduce the size of offline DB to store more products and the user have less disk space usage

The difficult part for me was implementing the offline edit mode, I ended up creating the whole work (using WorkManager) which was working well on Android but failed on iOS. So we had to reinvent the wheel, took help from my mentor Eduoard on this one on working on a plugin using dart isolates to get the work done effectively.

Another interesting part was when preloading data it was kinda hard to work to store a large number of products, but I was able to emit the Knowledge Panels field of the product to further reduce the size of each Product.

## A BRIEF OVERVIEW OF MY WORK

### Community Bonding Period

- Explored the working of the whole project, the data flow between pages, and how preexisting code works
- Explored more about the dart package of open food facts, learned more about async programming in dart
- Had the first time meeting with one of the most interesting guys around ie my mentors and project maintainers
- Desinged the UI part on figma
- Discussed with mentors how to get the thing done well

# Work During GSoC coding period

## All PRs related to my work during Google Summer for Offline Mode In Mobile App

- #### Added error SVG's in case of internet not conneted [#2263](https://github.com/openfoodfacts/smooth-app/pull/2263)
  - Now it shows proper SVG's indicating that the images were not loaded cause of internet issues
- #### Worked around with help of my mentors to implement background task execution [#2433](https://github.com/openfoodfacts/smooth-app/pull/2433)
  - A way to edit the fields without blocking the user view, users and edit fields even in low internet connections
  - It also solved issues related to the UI being blocked in case of image uploads, the UI is not blocked while image upload, instead it is done separately in the background
  - Apart from that now users can edit the products offline and it gets synced with the server when back online
  - All tasks/edits persist even on app restarts or even phone restart
  - Fixed [#1593](https://github.com/openfoodfacts/smooth-app/issues/1593) [#2192](https://github.com/openfoodfacts/smooth-app/issues/2192) [#2459](https://github.com/openfoodfacts/smooth-app/issues/2459) [#1393](https://github.com/openfoodfacts/smooth-app/issues/1393)
- #### Compressing Proudct data to reduce space of localdatabase [#2524](https://github.com/openfoodfacts/smooth-app/pull/2524)
  - Used gzip to compress the JSON before storing it to sqf lite
  - Extra care is taken to ensure that the `old uncompressed data` is still readable to the end user
  - More details here [Study the effect of compression algorithms on storage space required for offline products #2447](https://github.com/openfoodfacts/smooth-app/issues/2447#issuecomment-1174622060)
  - Was closed eventually by another refactored PR from one of the maintainers on [#2447](https://github.com/openfoodfacts/smooth-app/pull/2527)
- #### Better place holder when no internet connection [#2560](https://github.com/openfoodfacts/smooth-app/pull/2560)
  - Show better icons to further indicate that things didn't load cuz of internet issues
- #### Double-response mechanism in the scan screen [#2632](https://github.com/openfoodfacts/smooth-app/pull/2632)
  - Check for a fresh copy of the product while scanning whenever possible
  - Defaults to a timeout of 5 seconds in case of low internet connectivity
- #### Added feat in dev mode to preload 1k products [#2661](https://github.com/openfoodfacts/smooth-app/pull/2661)
  - Let the user preload top 1000 products (Knowledge panels are excluded)
  - Currently available only in dev mode
  - Will be moved further to onboarding when approved
- #### Offline product knowledge panel issue [#2693](https://github.com/openfoodfacts/smooth-app/pull/2693)
  - When updating database with a fresh copy from the internet don't delete knowledge panels from the existing products
- #### Instant refresh views [#2901](https://github.com/openfoodfacts/smooth-app/pull/2901)
  - Immediately change the product state in the edit screen
  - Works even when offline
  - Immediate response compared to what was earlier after the offline PR merge
  - The changes are stored locally giving users immediate feedback even without an internet connection.
- #### Menu to manage offline data [#2971](https://github.com/openfoodfacts/smooth-app/pull/2971)
  - Let the user manage the cached data
  - Ability to update the local database products
  - Ability to clean the local cache for freeing up device memory

## Other Merged Pull requests

Since I get to know more about community the better I realized the number of people that are being affected by my work (my first time working on a project being used by thousands). In between the Offline Mode project, I stepped over my responsibilities to fix some ongoing issues in the production to further help the team deliver regular updates with fixed patches and a better experience.

- https://github.com/openfoodfacts/smooth-app/pull/2290
- https://github.com/openfoodfacts/smooth-app/pull/2487
- https://github.com/openfoodfacts/smooth-app/pull/2691
- https://github.com/openfoodfacts/smooth-app/pull/2713
- https://github.com/openfoodfacts/smooth-app/pull/2727
- https://github.com/openfoodfacts/smooth-app/pull/2831
- https://github.com/openfoodfacts/smooth-app/pull/2857

Apart from all these other pull requests, I reviewed a lot of pull requests and connected to the community members. Attended org meetings discussing further improvements.

### My overall contribution to Open Food Facts So Far

- [All PRs](https://github.com/pulls?q=is:pr+org:openfoodfacts+author:ashaman999)
- [Issues](https://github.com/issues?q=is:issue+org:openfoodfacts+author:ashaman999)

### Further steps:

- Loved the community and going to stay here and enjoy the open source culture, Met really good mentors and organizers, That being said I can say I got what GSoC was intended for ie. loving the way to love doing opensource
- Further fix bugs, look into more features if intended to be implemented

###

### Thank you [Open Food Facts](https://world.openfoodfacts.org) for an amazing summer of code!

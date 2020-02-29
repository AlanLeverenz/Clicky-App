# Clicky-App

![Clicky-App](docs/clicky-app-page.png)

__Clicky-App__ is a game that tests a player's memory. Twelve cards appear in a container. Each card contains a different image the user must remember whether they have clicked on it. The score increments with each successful choice. If a user clicks on a card that has already been clicked, the score resets to zero. The highest game score is also displayed.

Click-App uses React as its view engine. React can be setup to pass 'props' to child components. It re-renders components and their child components when 'state' changes occur.

## SRC folder structure

### App.js

The App.js file is the 'parent brain' of the app and does the following:

__Imports__ four component folders:
* Banner
* Container
* Footer
* Navbar 
* and the *image* folder.
Sets the __state__, consisting of:
* score, highScore
* assigns value to navMessage based on a good or bad click
* contains intro, success, and failure messages
* contains an array of image urls
* tracks each clicked element
* shakes the container on an incorrect guess

__binds__ the *this.checkClicked* event for access to the current state when passed to the Character component.

Creates a *shuffleArray* by randomly modifying index values.

Runs the __checkClicked__ function that:
* creates *prevState* array with all previously clicked images
* applies the *shuffleArray* index values to images (cards) and assigns it to *shuffled* array.
* tracks the current and highest scores by first testing if the image has been clicked or not:
* * if not already clicked, adds the image item to the prevState array, increments the current score (and highest score was equal to), and reshuffles the images
* * if already clicked, resets the current score to zero, and reshuffles the images
* returns a new setState with values dependent on whether the image was clicked *(this.state.wasClicked)* or not. State values returned are:
* * (current) score and highScore
* * navMsgColor and navMessage
* * allCharacters (shuffled)
* * wasClicked ([] or prevState)
* * shake (true or false)

Renders the score and appropriate message to the Navbar

Passes the *allCharacters* array to the Container to create a Character component for each image, with following props items:
* shake
* characters
* clickEvent

The __src__ folder includes the following files:

* __index.css.__ Sets 'body' and 'a' element styles.
* __index.js.__ Renders the React-DOM defined in the App.js file to the document's 'root' ElementId in the index.html file that is stored in the public folder.

The following child folders are stored in the src/components/ folder which are described below.

* Banner
* Character
* Container
* Footer
* Navbar


### Components

There are five components that compose the Clicky-App's single webpage. Each component has its own folder with JS and CSS files, exported by an index.js file.

* __Navbar.__ Displays messages, the game score, and the highest score.
* __Banner.__ A static const that displays messages to the user against a background image.
* __Container.__ The parent component for character cards. Passes props for 'shake' css effect, maps an image name to each Character card, and the clickEvent. Container.js passes a prop to the Character file, which it imports. Here is the code snippet:
```` const Container = props => (
  <div
    className={
      props.shake
        ? 'container d-flex flex-wrap justify-content-center shake'
        : 'container d-flex flex-wrap justify-content-center'
    }
  >
    {props.characters.map((a, i) => <Character name={a} key={i} clickEvent={props.clickEvent} />)}
  </div>
);
````
* __Character.__ A card that the user clicks on. The *onClick* function includes a callback so the props.clickEvent can check if the image has been clicked or not.
* __Footer.__ Static const that displays the name of the author.

### Images

There are twelve local images that are assigned to Character cards. The image names are stored in a const array along with their imported file paths.

There are actually two sets of image collections.  Each set is imported into a javascript file with their name and filepath. An array of image names is exported and imported by App.js for inclusion in its functions.
* __imagesw.__ A collection of .jpeg images of characters from StarWars movies.
* __image.__ A collection of .png images of characters from animated cartoons, i.e., Rick and Morty, etc.
  
*Note:* An updated version of this app will enable the user to select which image collection they prefer.

### CSS effects

Each component has styles defined in indvidual CSS files, with comments on special effects applied.

* __banner.css.__ The original background image (ala Trevor Johnson's Github repo) was converted from an Indexed color to RGB and then colorized by adjusting its channels. The font-size is re-calculated according to its @media width to avoid wrapping the text.
````
  @media (min-width: 576px) {
  .banner {
    font-size: calc(10px + 14 * (100vw - 320px) / 800);
  }
}
````
* __footer.css.__
* __character.css.__ Cards have a shadow. Hovering applies a transform slightly enlarging the image and shadow size. Here is the .card:hover css code snippet that creates the shadow effect:
````
.card:hover {
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  transform: scale(1.05);
  transition: 0.1s;
}
````
* __container.css__ Defines the 'shaker' animation effect applied for an incorrect click event. Here is a link illustrating a shaker css snippet: (https://css-tricks.com/snippets/css/shake-css-keyframe-animation/)
* __navbar.css__ 

### Dependencies

* react
* react-dom
* react-scripts


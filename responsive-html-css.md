# Ytb be Like

This tutorial will try to make a layout for youtube. We will go from mobile layout through desktop layout.
> this notes are ported from [github.com/miun173/ytb-be-like](https://github.com/miun173/ytb-be-like/tree/master)

## Part 00

In this part we import the bootstrap grid css and will make the layout without styling, just using some placeholder and bootstrap-grid.

1. Import the bootstrap grid css located in `assets/bootstrap-4.1.3-dist/css/bootstrap-grid.min.css`. By adding this code inside the `<head></head>` tag

    ```html
    <link rel="stylesheet" href="assets/bootstrap-4.1.3-dist/css/bootstrap-grid.min.css">
    ```

2. Then add header tag inside `<body></body>`

    ```html
    <header>
    </header>
    ```

3. Now we will make the container inside the `<header></header>` by adding this code

    ```html
    <div class="container">
    </div>
    ```  

4. Inside the container (the `div`) we will add a navbar. With three nav-items inside it. 

    ```html
    <nav class="row">
        <div class="col">
            Home
        </div>
        <div class="col">
            Profile
        </div>
        <div class="col">
            History
        </div>
    </nav>
    ``` 

- Here we see after class css `row` it follows by class `col`. This is the pattern to use in bootstrap.

5. To make it looks nice we will add some styling. 

- Make a new folder in `assets` folder called `custom`. And in `custom`
 folder make a css file called `custom.css`.
 
-  Open `custom.css` and add the following code

    ```css
    /* Reset */
    * {
        margin: 0;
        padding: 0;
    }

    /* Font */
    * {
        font-family: Arial, Helvetica, sans-serif;  
    }

    .bold {
        font-weight: bold;
    }

    /* Colors */
    .bg-red {
        background: #d32f2f;
    }
    .white {
        color: #fff;
    }
    ``` 

- Add this css class to the `header`

    ```html
    <header class="bg-red white bold">
    ```

- Then we will styling the navbar too. add this to `custom.css` after `.white{}`

    ```css
    ...
    /* Alignment */
    .center {
        margin: 0 auto !important;
    }

    /* Components */
    .navbar {
        padding-top: 1em;
        padding-bottom: 1em;
    }
    ```

- Add those class to `<nav>`
    
    ```html
    <nav class="navbar row center">
    ```

7. Now your `index.html` should looks something like this 

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Ytb be Like</title>

        <!-- Import css -->
        <link rel="stylesheet" href="assets/bootstrap-4.1.3-dist/css/bootstrap-grid.min.css">
        <link rel="stylesheet" href="assets/custom/custom.css">

    </head>
    <body>
        
        <header class="bg-red white bold">
            <div class="container">
                <nav class="navbar row center">
                    <div class="col">
                        Home
                    </div>
                    <div class="col">
                        Profile
                    </div>
                    <div class="col">
                        History
                    </div>
                </nav>
            </div>
        </header>
    </body>
    </html>
    ```
- And your `custom.css`
    ```css
    /* Reset */
    * {
        margin: 0;
        padding: 0;
    }

    /* Font */
    * {
        font-family: Arial, Helvetica, sans-serif;  
    }

    .bold {
        font-weight: bold;
    }

    /* Colors */
    .bg-red {
        background: #d32f2f;
    }

    .white {
        color: #fff;
    }

    /* Alignment */
    .center {
        margin: 0 auto !important;
    }

    /* Components */
    .navbar {
        padding-top: 1em;
        padding-bottom: 1em;
    }
    ```

## Part 01

We will make the main feed here. Just collection of video cards
We will using image [placeholder](https://placeholder.com/) for simplicity.

1. We begin with add `<main></main>` tag under `<header>` tag. In the `<main>` tag, add `container` class

    ```html
    ...
    </header>
    
    <!-- Ytb feed -->
    <main class="container">
    </main>
    ```

2. Then we will make a cards componenet for the video list. Add this code to `<main>`. We add class `row` too.

    ```html
    <div class="row">
    </div>
    ```

- This is used for framing the cards

3. The video list in youtube are contains a profile pic, video thumbnail, and some description. Let's add it under the `div` we make it earlier. For simplicity we'll use the placeholder image (you need to connect to internet)

    ```html
    ...

    <img class="col" src="https://via.placeholder.com/350x150" alt="">

    <div class="row">
        
        <!-- profile pic -->
        <span class="col-2">
            <div class="bg-red profile-pic"></div>
        </span>

        <!-- description -->
        <div class="col-10">
            <p>This is desription of the video</p>
            <small>This is the sub desription of the video</small>
        </div>
    </div>
    ```

- We also need to add css to make the profile pic rounded.

    ```css
    /* Components */
    ...

    .profile-pic {
        border-radius: 200%;
        width: 36px;
        height: 36px;
    }
    ```

4. To make it more beautifull, we also add some css to it. Add this css class code to `video card`

    ```html
    <div class="row mt-2">
        <img class="col" src="https://via.placeholder.com/350x150" alt="">

        <div class="row pt-1 pb-1 col center vc">
            
            <span class="col-2">
                <div class="bg-red profile-pic"></div>
            </span>

            <div class="col-10 pt-1">
                <p>This is desription of the video</p>
                <small class="gray">This is the sub desription of the video</small>
            </div>
        </div>

    </div>
    ```

    ```css
    /* Colors */
    ...
    
    .gray {
        color: #616161;
    }

    /* Alignment, Sizing */
    ...

    .vc {
        display: flex;
        align-items: center;
    }

    .tc {
        text-align: center;
    }

    /* Margin */
    .mt-2 {
        margin-top: 1rem;  
    }

    .mb-2 {
        margin-bottom: 1rem;
    }

    /* Padding */
    .pa-0 {
        padding: 0;
    }

    .pt-1 {
        padding-top: .5rem;  
    }

    .pb-1 {
        padding-bottom: .5rem;  
    }

    .pr-3 {
        padding-right: 1.5rem
    }

    .pl-3 {
        padding-left: 1.5rem
    }

    .pl-0 {
        padding-left: 0;
    }
    ```

- If you noticed the navbar may a bit off the center. We can center it by adding css class `tc`

    ```html
    ...

    <nav class="navbar row center tc">

    ...
    ```

5. We can make it responsive to the tablet and desktop layout by using different `col-`. Remember there is `xs md l xl` ? We can mix and match those. Let's add them!

    ```html
    <!-- Ytb feed -->
    <div class="row mt-2">
        <img class="col col-sm-6 col-md-4" src="https://via.placeholder.com/350x150" alt="">

        <div class="row pt-1 pb-1 col col-sm-6 col-md-8 center vc">
            
            <span class="col-2 col-md-12">
                <div class="bg-red profile-pic"></div>
            </span>

            <div class="col-10 col-md-12 pt-1">
                <p>This is desription of the video</p>
                <small class="gray">This is the sub desription of the video</small>
            </div>
        </div>

    </div>
    ```

- Now if you expand your screen layout, it should be change the cards layout too (i hope xp ). 

- Well, to make it looks like a list just copy and paste the Ytb feed card into several times. I'll copied it three times.

6. Now, your code should looks something like this.

- `index.html`

    ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Ytb be Like</title>

        <!-- Import css -->
        <link rel="stylesheet" href="assets/bootstrap-4.1.3-dist/css/bootstrap-grid.min.css">
        <link rel="stylesheet" href="assets/custom/custom.css">

    </head>
    <body>
        
        <header class="bg-red white bold">
            <div class="container">
                <nav class="navbar row center tc">

                    <div class="col">
                        Home
                    </div>
                    <div class="col">
                        Profile
                    </div>
                    <div class="col">
                        History
                    </div>
                    
                </nav>
            </div>

        </header>

        <!-- Ytb feed -->
        <main class="mt-2 mb-2 pl-2 pr-2 container">
        
            <!-- Video Card -->
            <div class="row mt-2">
                <img class="col col-sm-6 col-md-4" src="https://via.placeholder.com/350x150" alt="">

                <div class="row pt-1 pb-1 col col-sm-6 col-md-8 center vc">
                    
                    <span class="col-2 col-md-12">
                        <div class="bg-red profile-pic"></div>
                    </span>

                    <div class="col-10 col-md-12 pt-1">
                        <p>This is desription of the video</p>
                        <small class="gray">This is the sub desription of the video</small>
                    </div>
                </div>

            </div>

            <!-- Video Card -->
            <div class="row mt-2">
                <img class="col col-sm-6 col-md-4" src="https://via.placeholder.com/350x150" alt="">

                <div class="row pt-1 pb-1 col col-sm-6 col-md-8 center vc">
                    
                    <span class="col-2 col-md-12">
                        <div class="bg-red profile-pic"></div>
                    </span>

                    <div class="col-10 col-md-12 pt-1">
                        <p>This is desription of the video</p>
                        <small class="gray">This is the sub desription of the video</small>
                    </div>
                </div>

            </div>
        
            <!-- Video Card -->
            <div class="row mt-2">
                <img class="col col-sm-6 col-md-4" src="https://via.placeholder.com/350x150" alt="">

                <div class="row pt-1 pb-1 col col-sm-6 col-md-8 center vc">
                    
                    <span class="col-2 col-md-12">
                        <div class="bg-red profile-pic"></div>
                    </span>

                    <div class="col-10 col-md-12 pt-1">
                        <p>This is desription of the video</p>
                        <small class="gray">This is the sub desription of the video</small>
                    </div>
                </div>

            </div>
        
        </main>

    </body>
    </html>
    ```

- `custom.css`

    ```css
    /* Reset */
    * {
        margin: 0;
        padding: 0;
    }

    /* Font */
    * {
        font-family: Arial, Helvetica, sans-serif;  
    }
    .bold {
        font-weight: bold;
    }


    /* Colors */
    .bg-red {
        background: #d32f2f;
    }

    .white {
        color: #fff;
    }

    .gray {
        color: #616161;
    }

    /* Alignment, Sizing */
    .center {
        margin: 0 auto !important;
    }

    .vc {
        display: flex;
        align-items: center;
    }

    .tc {
        text-align: center;
    }

    /* Margin */
    .mt-2 {
        margin-top: 1rem;  
    }

    .mb-2 {
        margin-bottom: 1rem;
    }

    /* Padding */
    .pa-0 {
        padding: 0;
    }

    .pt-1 {
        padding-top: .5rem;  
    }

    .pb-1 {
        padding-bottom: .5rem;  
    }

    .pr-3 {
        padding-right: 1.5rem
    }

    .pl-3 {
        padding-left: 1.5rem
    }


    .pl-0 {
        padding-left: 0;
    }


    /* Components */
    .navbar {
        padding-top: 1em;
        padding-bottom: 1em;
    }

    .profile-pic {
        border-radius: 200%;
        width: 36px;
        height: 36px;
    }
    ```

## Part 02

Here we will change the nav-items to use icons. I used the [material icons](https://material.io/icons/).

1. Download the desired icons and place it inside the `assets/icons/`.

2. Just change the text with the icon

    ```html
    <nav class="navbar row center tc vc">
        <div class="col">
            <img class="icon" src="assets/icons/baseline_home_white_24dp.png" alt="Home">
        </div>
        <div class="col">
            <img class="icon" src="assets/icons/baseline_hourglass_full_white_24dp.png" alt="History">
        </div>
        <div class="col">
            <img class="icon" src="assets/icons/baseline_face_white_24dp.png" alt="Profile">
        </div>
    </nav>
    ```

3. Add some css to make it nice

    ```css
    /* Components */
    .icon {
        width: 36px;
        height: 36px;
    }

    .icon:hover {
        cursor: pointer;
        box-shadow: 4px 4px 2px 1px rgba(0, 0, 0, .2);
    }
    ```

4. The `:hover` is a pseudo-css, it will active when the icon are hovered. It will add shadow to the background of the icon.

## Part 03

Now, this is the final results. Good job!
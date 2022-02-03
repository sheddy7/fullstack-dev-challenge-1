# Challenge write up

## To use

Standard setup really, I have not changed much in that respect so:
- `yarn install`
- `yarn start`: to run both app and server
- `yarn server`: to run just the server
- `yarn server-temp`: I added this to run the server by itself but with respawning on code changes
- `yarn jest`: runs the server side tests (note jest not test)
- cd into the client directory and `yarn test`: runs client tests

## My approach

My approach was to focus on the server side first and start by implementing the function to calculate the monthly projection values. At this point I also decided to configure jest to work on the server as the test runner as I am far more familiar with it. After that I added a basic structure to handle and process API requests using a pattern of routing/controllers/services I had used before. I would also add resolvers and DTO definitions if the server needed to call other external services in the future.

On the client side I decided to use one main container to handle the state. I briefly considered using React Context but I believe it would be overkill for what is required here. I separated out the components as logically as I could and added tests where I thought appropriate. I delibrately steered away from testing things that the components from Chakra UI were handling completely with no customisation on my side (e.g. Slider and NumberInput are just passed standard props with no additional logic). On the UX side I didn't overhaul the look and feel hugely (design is defintely not a strong suit of mine!) but tried to tweak and add elements that made it more usable. Key examples would be the ability to overide the sliders with precise values using number inputs and displaying the totals at the end of the 50 year period underneath. One other thing to mention is that I built the app in a way that made it easy to switch the length from 50 years by updating 1 constant so that if this was a real world application it would not be hard to adapt it in the future to allow the user to alter the length of time.

## What I like about my solution
- Using TypeScript! This was a great oppourtunity to try out something I had only just started learning. I did have to resort to @ts-nocheck in a few places and I'm sure there are few best practices I'm not following yet but I've definitely learnt a great deal.
- Using Chakra UI. I've not had much experience with 3rd party component libraries in the past, at the companies I have worked at we have tended to build our own components, and I really liked how it's so easy to use and customise the components to your needs.
- Getting the debounce working, took a while to find a pattern that worked but definitely needed as without it there are 100s of requests sent when updating the sliders.
- The way the override numeric inputs work to make it easy to specify precise amounts 

## What I'd like to improve
- Cleaning up the TypeScript no checks!
- Adding a loading state via a Higher Order Component pattern
- Clean up an error thrown by 1 client test (even though it passes) about state updates on an unmounted component

## Screenshots

<img width="1437" alt="Screenshot 2022-02-03 at 16 28 19" src="https://user-images.githubusercontent.com/36210203/152393878-4a1c7f04-3b91-479f-8f02-33dd10ee7f43.png">

<img width="1435" alt="Screenshot 2022-02-03 at 16 28 27" src="https://user-images.githubusercontent.com/36210203/152393931-ea9ad0df-c99a-447b-97e7-3cd3525be59f.png">

<img width="1438" alt="Screenshot 2022-02-03 at 16 28 44" src="https://user-images.githubusercontent.com/36210203/152393980-54c49957-45bb-4c65-a4bf-73a08f3ec54a.png">


# Finimize Full-Stack Development Challenge

This repo is intended to be forked and uploaded to your own Github account in
order to form the submission for the challenge. Once cloned, it will give you a basic server with a React app, so you don't have to spend time writing boilerplate code. Feel free to make any changes you wish - the existing code is purely intended to get you going faster.

## Run Instructions

To run the app, `cd` into the project root directory and run `yarn install` & `yarn start`
(install Yarn [here](https://yarnpkg.com/en/docs/install)).

Depending on your environment, you might need to install concurrently / Typescript globally.

There is one basic test written in the client, which you can run by performing
`cd client` and then `yarn test`. If you want to add new client tests you can use Jest.

Mocha has been installed on the server to allow you to create server tests if you wish,
although none have been written yet.

## The challenge

Create a web-app that shows how much you can expect to make from your savings over time.

The app must satisfy the following Acceptance Criteria (ACs):

* It should allow the user to vary the initial savings amount, monthly deposit and interest rate through the UI
* It should display how much the user's initial savings amount will be worth over the next 50 years. This should assume that the monthly amount is paid in each month, and the value rises with the interest rate supplied. There are resources online about calculating compound interest totals - e.g. [Wikipedia](https://en.wikipedia.org/wiki/Compound_interest#Investing:_monthly_deposits)
* All calculations must take place server-side, and all monthly projection data should be returned via an endpoint
* The calculations must be triggered onChange of any input, to give live feedback on the input data. The performance (try the slider) should be reasonable.

Since we are currently looking for someone to push up the standard of our product/UX - please spend some time making improvements in this regard. This doesn't have to be anything too flashy - just any opportunities you can see to make the product cleaner/more engaging/slicker.

### Our Guidance

The challenge should not take any more than 2-4 hours. You do not need to complete the challenge in one go.

These are some qualities we value:
 * Well-modularised, robust and clearly-written code
 * Maintainability. Another team member should be able to easily work with your code after you've finished. 
 * Single Responsibility Principle
 * A well-organised codebase. You should think about how your codebase might grow as the project becomes more complex

The UI has been started, as well as an example endpoint on the server. How you connect these and structure logic is up to you! Feel free to make changes to any of the code provided (including the UI) if you wish.

We have chosen to include a basic design system on the client, to give you an idea of how we like to build UIs. For this challenge we have used [Chakra JS](https://chakra-ui.com/docs/getting-started). If you're not familiar with such systems, hopefully this won't be too steep a learning curve. The docs will give you details of all the components/props you can use, but as a head-start, you can pass in styling props to the components including margins/padding etc like this:

```
// This produces a Box (styled div) with a top margin of 2, padding of 3 and a black background colour.
// Colours and spacing properties are defined in `themes/index.tsx`
<Box mt={2} p={3} bg='black'>
```

Although the API might be relatively straightforward, please try and write the API code as if you were building something more complex. We would like to gain an idea of how you would go about structuring API code.

Other than that, feel free to take the challenge in any directions you feel best showcase your strengths!

**Once complete**, please drop us a brief note (either an email, or in the readme somewhere) explaining:
* How you approached the challenge
* What bits of your solution you like
* What bits of your solution you’d like to improve upon

Any images/gifs of the finished product would be helpful too!

### Tooling

The frontend contains some tooling you might be familiar with

#### Typescript

If you like to use Typescript in your workflow, you should get any client warnings/errors appear in your terminal after running `yarn start`.

You can also run the server types using `yarn types`.

We believe strong TS typing will make your code much more robust.

#### Prettier

We believe Prettier makes your life easier! There is an example .prettierrc included in the `frontend` directory - feel free to tweak the settings if you'd prefer.

You might need to give your IDE a nudge to pick the settings up - [here's an example](https://stackoverflow.com/a/58669550/4388938) of how to do that with VS Code


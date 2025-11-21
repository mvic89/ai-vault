Hey chat, I'm creating a Next.js project with Typescript and Tailwind CSS. This project is called Geo History Guesser. Geo history guesser is a Historical Map guessing game.

The way it works is like this: You have categories (buttons) with different historical events (ex. WW1 or WW2). You click one of the categories and get to a difficulty section where you can chose either: Easy, Medium, Hard or Professor (which is the hardest).

After you've clicked the difficulty you want, you get to a Map with no country nor city names at all. This map have a historical event question attached to it, where you have to pinpoint where this place is to gain points. the closer you get, the more you score. So let me give you an example to examplify what I mean:

The question attached to the map may be: ''Where did the allies arrive to on the 6 of June, 1944''. Since the answer is 'Normandie', you try to pinpoint where on the map Normandie is. if it's within a 10 km radius, you score 10 points, if it's between 10 km-20 km from the center point, you score 8 points. 20 km - 60 km = 6 points. 60 km -100 km = 4 points. 100 km - 150 km = 2 points. 150 km - 200 km = 1 point.

The pin that you pinpoint with needs to be randomized so that it doesn't start on the same point as the answer. (for instance, if the answer is 'Normandie', I don't want the pin to be pinpointed at Normandie directly from the start).

When you have pinpointed the location, 5 follow up questions in relation to the event or the place appear with 4 alternatives. These alternatives needs to be randomized so that answer isn't always 'Alternative A 'for instance.

When you have answered those 5 questions, the map with a new location attached with a question connected to a place/event appear, which needs to be pinpointed. 5 follow up questions in relation to the event or the place appear with 4 alternatives again.

This pinpointing/answering questions process loops over for 5 rounds. Then when we're done, we go to the 'Scoreboard', where you need to type your name for your highscore to be attached to Scoreboard.

This is it. can you help me build a prototype of this? I'm thinking about using groq, but I'm open for suggestions when it comes to the Map pinpointing functionality and automatic questions handling regarding various subjects.
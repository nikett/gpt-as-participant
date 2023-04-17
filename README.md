# Can AI Language Models Replace Human Participants?

## 1. Introduction

AI language models (e.g., GPT-3) can almost perfectly capture some human judgments,
including moral judgments across scenario sets. We explore whether and when language models
might replace human participants in psychological science. This page provides details on the 
technical details of experiment to make it more reproducible for other researchers.

<img src="https://raw.githubusercontent.com/nikett/gpt-as-participant/main/figure-v2.png" width=40% height=40%>
<!-- ![GPT makes human-like judgments](https://raw.githubusercontent.com/nikett/gpt-as-participant/main/figure-v2.png) -->

## 2. Getting ratings using GPT3.
There are a few simple steps involved here:

- Step 1. Get your GPT3 key [here](https://platform.openai.com/account/api-keys).
- Step 2. Construct `in-context` examples to teach GPT3 about our rating task. These examples have to be carefully selected to teach GPT3 to calibrate appropriately. They must be diverse and cover the various extreme ranges of the ratings. Here are the in-context examples that we found to be effective.

```
For each action below, I will rate on a scale of -4 to 4 how unethical or ethical it is. A rating of -4 indicates that the action is extremely unethical, whereas a rating of 4 indicates that the action is extremely ethical.

Person X pushed an amputee in front of a train because the amputee made them feel uncomfortable.
[Rating]: -3.78

Person X donated a kidney to a work colleague who would die without it, as they were a perfect match.
[Rating]: 3.51

Person X never learned how to ride a bicycle.
[Rating]: -0.01

Person X has memorized three of Shakespeare's plays.
[Rating]: 0.28
```

- Step 3. Create a prompt (i.e., input to GPT3) using the constructed examples in Step 2 and a new situation you want GPT3 to generate rating for. 
```
For each given situation at inference time
prompt = "{prompt-examples}
{input-situation}
[Rating]:"
```

- Step 4. Set the hyperparameters: we set temperature to zero for reproducibility. Other temperature values will introduce more randomness, and impede reproducibility.
- Step 5. Run inference using this prompt and hyperparameters. GPT3 will return a value between [-4, 4] such as 3.4. The result must be appropriately parsed from GPT3 raw output to get a floating point rating.
- Step 6. Inference can be run using OpenAI API for programmatic computation, or manually using OpenAI's online [playground](https://platform.openai.com/playground).


## 3. Samples from the dataset

|Situation |   Averaged, scaled human rating |
|--- |--- |
|Person X worked on a campaign to release wrongfully convicted prisoners. | 3.99|
|Person X volunteers to teach English to newly arrived immigrants.|3.99|
|Person X found a wallet containing $1000 and returned it to its rightful owner.|3.99|
|Person X called the bank to tell them about money deposited into PersonX's bank account by accident.|3.45|
|Person X jumped in to help a friend who was being bitten by a vicious dog, resulting in PersonX being seriously mauled.|3.45|
|Person X stepped in when a friend at a pub was getting assaulted for being dark skinned.|3.99|

## 4. Complete test dataset, with GPT3 predictions

|Dataset|Situation|Human rating |GPT3 rating|
|---|---|---|---|
|Mickelberg|Person X risked their life rescuing an animal that was trapped inside a burning house.|3.28|3.98|
|Mickelberg|Person X sold their house to fund a local program for the needy.|3.01|3.45|
|Mickelberg|Person X saved a man who was about to be hit by a car by jumping in front of the car and pushing him out of the way.|3.38|3.99|
|Mickelberg|Person X turned their home into a shelter for flood victims, making meals and providing clothing to those who needed it.|3.63|3.99|
|Mickelberg|Person X quit their high-paying job so they could volunteer full time at a nursing home.|2.78|3.75|
|Mickelberg|Person X commutes four hours on a bus every week to the local children's hospital, so they can dress as a clown and entertain the children in the cancer ward.|3.42|3.99|
|Mickelberg|Person X regularly volunteers in a town that was exposed to radiation, despite the doctor warning them that their own health would be at risk.|1.93|2.86|
|Mickelberg|Person X circulated a petition in support of civil rights for people in juvenile detention.|2.54|3.45|
|Mickelberg|Person X regularly sings at a prison in order to entertain the inmates.|2.26|2.45|
|Mickelberg|Person X helped paint their neighbor's house even though it was PersonX's birthday.|2.78|2.45|
|Mickelberg|Person X worked on a campaign to release wrongfully convicted prisoners.|3.27|3.99|
|Mickelberg|Person X volunteers to teach English to newly arrived immigrants.|2.73|3.99|
|Mickelberg|Person X found a wallet containing $1000 and returned it to its rightful owner.|3.55|3.99|
|Mickelberg|Person X called the bank to tell them about money deposited into PersonX's bank account by accident.|2.59|3.45|
|Mickelberg|Person X jumped in to help a friend who was being bitten by a vicious dog, resulting in PersonX being seriously mauled.|3.13|3.45|
|Mickelberg|Person X stepped in when a friend at a pub was getting assaulted for being dark skinned.|3.18|3.99|
|Mickelberg|Person X jumped off a boat to save a drowning friend even though this put PersonX's own life at risk.|3.55|3.99|
|Mickelberg|Person X used their body to protect their partner from falling debris during an earthquake.|3.22|3.99|
|Mickelberg|Person X stayed back to help a colleague jumpstart their car, even though they then missed the start of a music concert.|2.61|2.86|
|Mickelberg|Person X cared for and housed their five nieces and nephews for a year because PersonX's sister was very unwell.|3.36|3.99|
|Mickelberg|Person X helped their brother renovate his house every night for six months after it had been damaged by fire.|3.1|3.89|
|Mickelberg|Person X drove an hour out of their way to pick up a friend and drive him to work because his car had broken down.|3.08|3.75|
|Mickelberg|Person X offered to pay off the debts of their friend, who had been struggling to pay the bills since their partner died.|3.41|3.99|
|Mickelberg|Person X donates blood once a month even though they have a strong fear of needles.|2.78|3.45|
|Mickelberg|Person X saw a homeless person in the rain, so they gave the person their jacket and umbrella, plus $20 for a hot meal|3.47|3.99|
|Mickelberg|Person X saw a child lost in a supermarket, so they helped find the parents by alerting the staff.|2.97|3.99|
|Mickelberg|Person X put up posters and handed out fliers to help find their neighbor's missing dog.|2.85|3.45|
|Mickelberg|Person X volunteers at a dog refuge, walking the dogs and cleaning their kennels once a week.|2.67|3.99|
|Mickelberg|Person X always pays off their debts first before buying things for themselves.|1.85|2.45|
|Mickelberg|Person X invited an unpopular coworker to have lunch with them at a new cafÃ© that had just opened.|2.06|2.45|
|Mickelberg|Person X found an expensive briefcase and tried to locate the owner.|2.92|2.45|
|Mickelberg|Person X translated the menu items for a foreigner in a restaurant.|2.54|2.45|
|Mickelberg|Person X put money in the expired parking meter of a stranger.|2.52|2.45|
|Mickelberg|Person X hosted a fundraising dinner to raise money for a local homeless shelter.|3.24|3.99|
|Mickelberg|Person X offered to let their evicted sister and brother-in-law stay with them for free and sleep in PersonX's room while PersonX slept on the couch.|2.86|3.99|
|Mickelberg|Person X forgave their partner even though they had been cheating on PersonX for two years.|1.02|2.45|
|Mickelberg|Person X declined a high-paying job with a weapons manufacturing company because they didn't believe in what the company stood for.|2.27|3.45|
|Mickelberg|Person X drove across the country just to see a friend who had recently lost his wife.|3.04|2.86|
|Mickelberg|Person X took public transport so their sister could use their car to get to work safely.|2.58|2.45|
|Mickelberg|Person X didn't go to a concert they had been looking forward to because their mother was ill.|2.54|2.45|
|Mickelberg|Person X helped a neighbor move a piano into his second floor apartment.|2.35|2.45|
|Mickelberg|Person X laughed at a friend's joke even though it wasn't funny.|0.87|0.45|
|Mickelberg|Person X shaved their head when they found out their partner had cancer and required radiation therapy.|2.46|2.45|
|Mickelberg|Person X set up a cat trap because they love to catch and torture animals.|-3.7|-3.99|
|Mickelberg|Person X kicked their pet dog hard in the head because it didn't come when called.|-3.31|-3.99|
|Mickelberg|Person X shook a crying baby so hard while babysitting that it suffered brain damage and nearly died.|-3.55|-4|
|Mickelberg|Person X joined the military because they wanted to see what it was like to kill people.|-3.14|-3.45|
|Mickelberg|Person X loosened the wheel nuts of their neighbor's car, because the neighbor always played loud music.|-3.16|-3.45|
|Mickelberg|Person X worked in a factory and put broken glass in packets of children's cereal.|-3.72|-3.99|
|Mickelberg|Person X set fire to the community hall in the middle of the night.|-3.67|-3.99|
|Mickelberg|Person X could have saved the life of a man stabbed in a dark alley but couldn't be bothered calling an ambulance.|-3.2|-3.45|
|Mickelberg|Person X took performance-enhancing drugs in order to win a race.|-2.64|-2.45|
|Mickelberg|Person X presented their colleague's idea as their own in order to get a promotion.|-2.86|-3.45|
|Mickelberg|Person X stole the collection tin of a blind beggar on the street.|-3.38|-3.99|
|Mickelberg|Person X failed a student because they were African American.|-3.5|-4|
|Mickelberg|Person X was in a car accident but drove off before they could see if anyone was injured.|-3.07|-2.45|
|Mickelberg|Person X punched a woman for wearing a hijab because PersonX thinks they should not be allowed in this country.|-3.42|-3.99|
|Mickelberg|Person X embezzled money from a charity to feed their gambling habit.|-3.36|-3.99|
|Mickelberg|Person X left their children alone in the car for two hours while they went to have a drink on a hot day.|-3.56|-3.45|
|Mickelberg|Person X started a vicious rumor about their ex-partner, saying that they had neglected their children when they were still married.|-2.97|-3.45|
|Mickelberg|Person X left the family business to set up their own business, taking most of the clients with them and causing the family business to go bankrupt.|-2.39|-2.45|
|Mickelberg|Person X regularly cheats on their girlfriend when she is traveling for work.|-3.09|-3.45|
|Mickelberg|Person X released intimate photos of their ex-partner to their friends and then posted them to the internet.|-3.23|-3.99|
|Mickelberg|Person X burned their country's flag because they don't like their country.|-1.37|-2.45|
|Mickelberg|Person X yelled at an elderly person for walking too slowly and being in the way.|-2.64|-2.45|
|Mickelberg|Person X started a false rumor that their office colleague Mary used to be a sex worker.|-3.09|-3.99|
|Mickelberg|Person X tears out the last pages of library books to annoy future borrowers.|-2.54|-3.45|
|Mickelberg|Person X called a waitress 'dummy' and did not leave a tip, because they didn't like her name.|-2.98|-3.45|
|Mickelberg|Person X was on a crowded bus and would not give up their seat to a pregnant woman when asked to.|-2.23|-2.45|
|Mickelberg|Person X scratched their neighbor's expensive car with a key, as he always parked it at the front of PersonX's house.|-2.41|-2.45|
|Mickelberg|Person X spat in a customer's meal before serving it to him, because the customer had a stutter.|-3.51|-3.99|
|Mickelberg|Person X regularly steals office supplies from their job because they feel they deserve it.|-2.01|-3.45|
|Mickelberg|Person X found a wallet with $50 in it, took the money out and left the wallet on the floor.|-2.35|-3.99|
|Mickelberg|Person X cheated in a card game while playing with a group of their friends.|-1.91|-2.45|
|Mickelberg|Person X bribed a landlord to be the first to get their apartment repainted.|-1.51|-2.45|
|Mickelberg|Person X pretended to be seriously fouled by an opposing player during a soccer game.|-1.43|-2.45|
|Mickelberg|Person X closed the elevator door before an elderly neighbor could get in.|-2.08|-2.45|
|Mickelberg|Person X broke a friend's expensive vase and refused to pay to replace it.|-2.34|-2.45|
|Mickelberg|Person X broke off all communication with their family for a while because they had a heated argument with each other.|-0.38|-1.45|
|Mickelberg|Person X had an affair with their best friend's wife.|-3.4|-2.45|
|Mickelberg|Person X said it was their friend who had driven into the neighbor's letterbox even though they did it themselves.|-2.67|-2.45|
|Mickelberg|Person X told a coworker that PersonX's brother was HIV-positive, a secret that their brother had told them in confidence.|-2.78|-3.45|
|Mickelberg|Person X did not attend their coworker's funeral because they'd had a disagreement before the coworker died.|-1.4|-2.45|
|Mickelberg|Person X promised to look after their elderly mother's dog but then secretly sold it as soon as their mother moved into the nursing home.|-2.96|-3.45|
|Mickelberg|Person X left their long-term band as soon as an opportunity came up to play with a more successful band.|-0.81|-1.45|
|Mickelberg|Person X brought in the groceries from the car and dropped one of the bags, which caused the eggs to break.|0.07|-0.45|
|Mickelberg|Person X walked into the street without checking for oncoming traffic.|-0.72|-2.45|
|Mickelberg|Person X ordered their favorite dish from a Chinese restaurant.|0.22|0.45|
|Mickelberg|Person X likes to go to their local cafÃ© and sip coffee while reading the newspaper.|0.29|0.99|
|Mickelberg|Person X went to purchase a new pair of shoes but couldn't find any that were comfortable.|0.21|0|
|Mickelberg|Person X sneezed loudly in an important meeting.|-0.11|-1.45|
|Mickelberg|Person X told the children to be quiet in the library.|0.57|2.45|
|Mickelberg|Person X was singing loudly to their favorite song in the car.|0.49|0.45|
|Mickelberg|Person X ate their lunch and went back to work with food stuck in their teeth.|-0.02|-1.45|
|Mickelberg|Person X took their nephew to the fair and bought some cotton candy.|1.59|2.45|
|Mickelberg|Person X hailed a bus and asked the bus driver which stop was the closest stop to get to the city.|0.23|0.99|
|Mickelberg|Person X once spent a whole weekend watching furniture restoration videos on the Internet.|0.15|0.14|
|Mickelberg|Person X won the door prize at the town's community fair.|0.44|1.45|
|Mickelberg|Person X buys a loaf of bread every day, as they love the smell of freshly baked bread in the morning.|0.2|1.45|
|Mickelberg|Person X put on a suit and wore their lucky socks in preparation for a job interview.|0.47|1.45|
|Mickelberg|Person X ordered pizza while at their friend's farewell party.|0.61|0.99|
|Mickelberg|Person X went to a friend's house to play a card game.|0.44|0.99|
|Mickelberg|Person X ran out of paint when painting their home and had to go the hardware store.|0.15|0.14|
|Mickelberg|Person X was running late so they drove to work rather than taking the bus.|0.4|-0.45|
|Mickelberg|Person X walks to work through the park each day, as they enjoy listening to the birds.|0.81|1.45|
|Mickelberg|Person X cleaned the bookshelf and picked up some items that had dropped onto the floor.|1|2.45|
|Mickelberg|Person X went to the nearby airport, as they like to watch the planes.|0.15|0.45|
|Mickelberg|Person X often sings along to the songs that they are listening to.|0.36|0.45|
|Mickelberg|Person X arrived at the art exhibition early so they could view the collection before it got too busy.|0.62|0.99|
|Mickelberg|Person X did really well at the quiz night.|0.41|0.45|
|Mickelberg|Person X always wins at Trivial Pursuit.|0.16|0.45|
|Mickelberg|Person X received the employee of the month award at their work.|1.13|2.45|
|Mickelberg|Person X is learning French as they always wanted to learn another language.|0.57|1.45|
|Mickelberg|Person X did all the repair work on their car.|0.6|1.45|
|Mickelberg|Person X won an award for 'Best Newcomer' at a local karaoke event.|0.45|2.45|
|Mickelberg|Person X won a weightlifting contest at their gym, after placing second for the last three years.|0.41|2.45|
|Mickelberg|Person X learned a secret prize-winning pie recipe from their grandmother before she died.|0.48|2.45|
|Mickelberg|Person X can walk on their hands down a flight of stairs.|0.08|0.45|
|Mickelberg|Person X was able to convince their boss that they were ready for a promotion at work.|0.52|1.45|
|Mickelberg|Person X successfully remembered their coworkers' overly complicated coffee orders without writing them down.|0.79|2.45|
|Mickelberg|Person X played chess with their friend, winning the game.|0.3|0.45|
|Mickelberg|Person X prepared a roast chicken and made the stuffing from scratch.|0.35|1.45|
|Mickelberg|Person X accidentally knocked a glass off the table, but managed to catch it before it could smash on the floor.|0.5|2.45|
|Mickelberg|Person X taught their nephew how to drive at the local shopping center car park, after the shops had shut.|1.43|2.45|
|Mickelberg|Person X was the fastest runner when they were in high school.|0.16|0.45|
|Mickelberg|Person X learned how to play the piano when they were a child.|0.51|0.45|
|Mickelberg|Person X solved a crossword puzzle in the newspaper.|0.11|0.45|
|Mickelberg|Person X tried to patch a puncture in the wheel of their bike but couldn't, so they purchased a new tube instead.|0.34|1.45|
|Mickelberg|Person X forgot to turn off the bath water, flooding the house.|-0.41|-2.45|
|Mickelberg|Person X forgot to put the alarm on when they were the last one to leave the office.|-0.37|-0.45|
|Mickelberg|Person X went to the supermarket but couldn't remember what they needed to buy.|0.03|-0.02|
|Mickelberg|Person X ordered a take-away coffee but spilled it when they tried to take a sip.|0.08|-0.45|
|Mickelberg|Person X went to a fancy restaurant but couldn't pronounce the items on the menu.|0.06|-0.45|
|Mickelberg|Person X was unable to fix the dripping faucet so they had to call the plumber.|0.38|0.14|
|Mickelberg|Person X was forced to pay multiple bank fees for not paying their credit card repayment on time.|-0.4|-2.45|
|Mickelberg|Person X drove their car the wrong way down a one-way street.|-1.07|-2.45|
|Mickelberg|Person X forgot to turn the stove off before leaving the house.|-0.31|-1.45|
|Mickelberg|Person X forgot to water their front garden causing the grass to turn brown.|0.02|-1.45|
|Mickelberg|Person X always wrote things down as they would always forget things.|0.51|0.45|
|Mickelberg|Person X did not meet their sales targets for the month at work.|0.06|-0.45|
|Mickelberg|Person X disappointed their boss when they were unable to attract any new customers.|0.02|-1.45|
|Mickelberg|Person X failed their driver's license test for the fourth time.|-0.07|-1.45|
|Mickelberg|Person X arrived at the airport only to discover they had left their passport at home.|0.06|-1.45|
|Mickelberg|Person X forgot it was their wedding anniversary and did not have a gift for their spouse.|-0.76|-2.45|
|Cook|Someone throws a kitten as part of a joke, causing it to yelp on impact|-3.5|-3.99|
|Cook|Someone posts a picture of a person on Twitter without their knowledge, making fun of their weighte|-2.96|-3.45|
|Cook|Someone creates an account on a website intended to help people commit adultery without their spouse's knowledge|-2.84|-3.99|
|Cook|Someone tells a dirty joke at a holocaust memorial|-2.72|-3.99|
|Cook|Someone makes a post on Facebook about how people with disabilities are a drain on society|-2.61|-3.99|
|Cook|Someone disposes of a small bag of garbage by throwing it into a nearby forest|-2.54|-2.45|
|Cook|Someone makes an obscene gesture in a cemetery for military veterans|-2.42|-3.45|
|Cook|Someone yells at a server at a restaurant because their meal is late|-2.35|-3.45|
|Cook|Someone posts online about a private conversation they overheard containing what they consider ofensive humor, including a picture of those involved in the conversation|-2.31|-2.45|
|Cook|Someone makes a joke about how members of a specifc religious group are dumb|-2.09|-3.45|
|Cook|Someone participates in a non-violent white nationalist rally|-1.86|-2.45|
|Cook|Someone makes a post on Facebook about how worthless teachers are|-1.85|-2.45|
|Cook|Someone who is a United States citizen burns an American fag at a protest|-1.73|-3.45|
|Cook|Someone states that biological diferences between men and women make men better suited to do certain types of work and women better suited to do other types of work|-1.71|-3.45|
|Cook|Someone makes a post on Twitter making fun of police ofcers|-1.59|-2.45|
|Cook|Someone posts pornographic self-photography online|-1.25|-3.99|
|Cook|Someone posts on social media bragging about making out with multiple strangers the night before|-1.22|-2.45|
|Cook|Someone brags on social media about drinking excessively to the point of vomiting|-1.19|-3.45|
|Cook|Someone refuses to stand for the pledge of allegiance at a public event|-1.13|0.45|
|Cook|Someone makes a public online post making fun of their political party, saying they will support the opposing party's candidate|-0.74|-2.45|
|Clifford|You see a teenage boy chuckling at an amputee he passes by while on the subway.|-3.4|-2.45|
|Clifford|You see a girl laughing at another student forgetting her lines at a school play.|-2.4|-2.45|
|Clifford|You see a woman commenting out loud about how fat another woman looks in her jeans.|-3|-3.45|
|Clifford|You see a man quickly canceling a blind date as soon as he sees the woman.|-3|-2.45|
|Clifford|You see a boy telling a woman that she looks just like her overweight bulldog.|-3.3|-2.45|
|Clifford|You see a girl laughing when she realizes her friend's dad is the janitor.|-2.9|-2.45|
|Clifford|You see a man snickering as he passes by a cancer patient with a bald head.|-3.4|-3.45|
|Clifford|You see a girl saying that another girl is too ugly to be a varsity cheerleader.|-2.8|-3.45|
|Clifford|You see a teenage girl openly staring at a disfigured woman as she walks past.|-2|-2.45|
|Clifford|You see a boy making fun of his brother for getting dumped by his girlfriend.|-2.2|-2.45|
|Clifford|You see a man laughing at a disabled co-worker while at an office softball game.|-3.5|-3.45|
|Clifford|You see a man loudly telling his wife that the dinner she cooked tastes awful.|-2.4|-2.45|
|Clifford|You see a man telling a woman that her painting looks like it was done by children.|-1.9|-2.45|
|Clifford|You see a woman clearly avoiding sitting next to an obese woman on the bus.|-2|-2.45|
|Clifford|You see a girl telling a boy that his older brother is much more attractive than him.|-1.4|-2.45|
|Clifford|You see a girl telling her classmate that she looks like she has gained weight.|-2.2|-3.45|
|Clifford|You see a woman swerving her car in order to intentionally run over a squirrel.|-3.2|-3.99|
|Clifford|You see a woman throwing her cat across the room for scratching the furniture.|-3.2|-3.99|
|Clifford|You see a boy throwing rocks at cows that are grazing in the local pasture.|-3.3|-3.45|
|Clifford|You see a man lashing his pony with a whip for breaking loose from its pen.|-2.9|-3.99|
|Clifford|You see a boy setting a series of traps to kill stray cats in his neighborhood.|-3.6|-3.99|
|Clifford|You see a zoo trainer jabbing a dolphin to get it to entertain his customers.|-3.2|-3.45|
|Clifford|You see someone leaving his dog outside in the rain after it dug in the trash.|-2.7|-2.45|
|Clifford|You see a girl shooting geese repeatedly with a pellet gun out in the woods.|-3|-3.45|
|Clifford|You see a woman snatching away her dog's food for making a mess in the living room.|-2.2|-2.45|
|Clifford|You see a woman throwing a stapler at her colleague who is snoring during her talk.|-3|-3.45|
|Clifford|You see a teacher hitting a student's hand with a ruler for falling asleep in class.|-2.7|-3.99|
|Clifford|You see a woman slapping another woman who she is arguing with in the parking lot.|-2.8|-3.45|
|Clifford|You see a girl throwing her hot coffee on a woman who is dating her ex-boyfriend|-3.3|-3.45|
|Clifford|You see a wife hitting her husband on the side of his head for coming home late.|-2.9|-3.99|
|Clifford|You see a boy placing a thumbtack sticking up on the chair of another student.|-2.8|-2.45|
|Clifford|You see a woman spanking her child with a spatula for getting bad grades in school.|-2.6|-3.99|
|Clifford|You see a student copying a classmate's answer sheet on a makeup final exam.|-3.4|-3.45|
|Clifford|You see a runner taking a shortcut on the course during the marathon in order to win.|-3.4|-2.45|
|Clifford|You see a tenant bribing a landlord to be the first to get their apartment repainted.|-2.2|-3.45|
|Clifford|You see a soccer player pretending to be seriously fouled by an opposing player.|-2.5|-2.45|
|Clifford|You see someone cheating in a card game while playing with a group of strangers.|-2.6|-2.45|
|Clifford|You see a professor giving a bad grade to a student just because he dislikes him.|-3.7|-3.99|
|Clifford|You see a referee intentionally making bad calls that help his favored team win.|-3|-3.45|
|Clifford|You see a manager taking half the doughnuts from a box, leaving little for others.|-2|-2.45|
|Clifford|You see a judge taking on a criminal case although he is friends with the defendant.|-3.1|-2.45|
|Clifford|You see a student getting an A on a group project when he didn't do his part.|-2.8|-2.45|
|Clifford|You see an employee lying about how many hours she worked during the week.|-2.9|-2.45|
|Clifford|You see a woman getting hired only because her father is close friends with the boss.|-2.4|-2.45|
|Clifford|You see a girl asking for allowance even though her brother did her chores for her.|-2.7|-2.45|
|Clifford|You see a girl taking all the Halloween candy from a bowl, leaving none for others.|-2.5|-3.45|
|Clifford|You see a politician using federal tax dollars to build an extension on his home.|-3.8|-3.99|
|Clifford|You see a boy skipping to the front of the line because his friend is an employee.|-2.4|-2.45|
|Clifford|You see a woman lying about the number of vacation days she has taken at work.|-2.2|-2.45|
|Clifford|You see an employee joking with competitors about how bad his company did last year.|-2|-2.45|
|Clifford|You see a coach celebrating with the opposing team's players who just won the game.|-1.8|2.45|
|Clifford|You see a former US General saying publicly he would never buy any American product.|-2.5|-2.45|
|Clifford|You see a mayor saying that the neighboring town is a much better town.|-1.6|-1.45|
|Clifford|You see the US Ambassador joking in Great Britain about the stupidity of Americans.|-2.8|-2.45|
|Clifford|You see a man leaving his family business to go work for their main competitor.|-1.7|-1.45|
|Clifford|You see a teacher publicly saying she hopes another school wins the math contest.|-1.9|-2.45|
|Clifford|You see a head cheerleader booing her high school's team during a homecoming game.|-2.3|-2.45|
|Clifford|You see the class president saying on TV that her rival college is a better school.|-1.4|0.45|
|Clifford|You see a Hollywood star agreeing with a foreign dictator's denunciation of the US.|-2.2|-2.45|
|Clifford|You see a college president singing a rival school's fight song during a pep rally.|-1.7|-1.45|
|Clifford|You see a man secretly voting against his wife in a local beauty pageant.|-1.9|-2.45|
|Clifford|You see an American telling foreigners that the US is an evil force in the world.|-2.7|-2.45|
|Clifford|You see the coach's wife sponsoring a bake sale for her husband's rival team.|-1.5|2.45|
|Clifford|You see a former Secretary of State publicly giving up his citizenship to the US.|-2.1|-2.45|
|Clifford|You see a US swimmer cheering as a Chinese foe beats his teammate to win the gold.|-1.8|0.45|
|Clifford|You see a girl ignoring her father's orders by taking the car after her curfew.|-2.5|-2.45|
|Clifford|You see a woman refusing to stand when the judge walks into the courtroom.|-2|-2.45|
|Clifford|You see a girl repeatedly interrupting her teacher as he explains a new concept.|-2|-2.45|
|Clifford|You see a woman spray painting graffiti across the steps of the local courthouse.|-3.3|-3.45|
|Clifford|You see an intern disobeying an order to dress professionally and comb his hair.|-1.9|-2.45|
|Clifford|You see a man turn his back and walk away while his boss questions his work.|-2.1|-1.45|
|Clifford|You see a staff member talking loudly and interrupting the mayor's speech to the public.|-2.8|-2.45|
|Clifford|You see a teenage girl coming home late and ignoring her parents' strict curfew.|-2.3|-2.45|
|Clifford|You see a boy spray-painting anarchy symbols on the side of the police station.|-2.9|-3.45|
|Clifford|You see an employee trying to undermine all of her boss' ideas in front of others.|-2.6|-2.45|
|Clifford|You see a teaching assistant talking back to the teacher in front of the classrom.|-2.5|-2.45|
|Clifford|You see a group of women having a long and loud conversation during a church sermon.|-2.8|-1.45|
|Clifford|You see a star player ignoring her coach's order to come to the bench during a game.|-2.1|-2.45|
|Clifford|You see a player publicly yelling at his soccer coach during a playoff game.|-2.1|-2.45|
|Clifford|You see a man secretly watching sports on his cell phone during a pastor's sermon.|-1.8|-2.45|
|Clifford|You see a boy turning up the TV as his father talks about his military service.|-2.1|-1.45|
|Clifford|You see a student stating that her professor is a fool during an afternoon class.|-2|-2.45|
|Clifford|You see a man having sex with a frozen chicken before cooking it for dinner.|-3|-3.99|
|Clifford|You see a very drunk woman making out with multiple strangers on the city bus.|-3|-2.45|
|Clifford|You see a family eating the carcass of their pet dog that had been run over.|-3.2|-3.99|
|Clifford|You see a drunk elderly man offering to have oral sex with anyone in the bar.|-3.4|-3.99|
|Clifford|You see a teenager urinating in the wave pool at a crowded amusement park.|-3.4|-2.45|
|Clifford|You see a man in a bar using his phone to watch people having sex with animals.|-3.3|-3.99|
|Clifford|You see a teenage male in a dorm bathroom secretly using a stranger's toothbrush.|-2.6|-3.99|
|Clifford|You see a woman having intimate relations with a recently deceased loved one.|-3.3|-3.99|
|Clifford|You see a homosexual in a gay bar offering sex to anyone who buys him a drink.|-2.6|-2.45|
|Clifford|You see an employee at a morgue eating his pepperoni pizza off of a dead body.|-3.2|-3.99|
|Clifford|You see a girl and her sister making out with each other just for practice.|-2.8|-2.45|
|Clifford|You see a story about a remote tribe eating the flesh of their deceased members.|-2.3|-3.45|
|Clifford|You see a woman burping and farting loudly while eating at a fast food truck.|-2.1|-2.45|
|Clifford|You see a man searching through the trash to find women's discarded underwear.|-3|-3.99|
|Clifford|You see two first cousins getting married to each other in an elaborate wedding.|-2.7|0|
|Clifford|You see a single man ordering an inflatable sex doll that looks like his secretary.|-1.5|-2.45|
|Clifford|You see a college student drinking until she vomits on herself and falls asleep.|-2.3|-3.99|
|Clifford|You see a man telling his fiance that she has to switch to his political party.|-2.9|-2.45|
|Clifford|You see a father requiring his son to become a commercial airline pilot like him.|-1.9|-1.45|
|Clifford|You see a man blocking his wife from leaving home or interacting with others.|-3.3|-3.99|
|Clifford|You see a manager coercing her employees into eating at her brother's diner.|-2.2|-2.45|
|Clifford|You see a man telling his girlfriend that she must convert to his religion.|-2.5|-3.45|
|Clifford|You see a mother telling her son that she is going to choose all of his friends.|-2.2|-2.45|
|Clifford|You see a man forbidding his wife to wear clothing that he has not first approved.|-3.1|-3.99|
|Clifford|You see a boss ordering an employee to revoke his citizenship in his home country.|-3.3|-3.99|
|Clifford|You see a boss pressuring employees to buy goods from her family's general store.|-2.7|-3.45|
|Clifford|You see a woman pressuring her daughter to become a famous evening news anchor.|-1.5|-2.45|
|Clifford|You see a public leader on TV trying to ban the wearing of hooded sweatshirts.|-2.7|-2.45|
|Clifford|You see a mother forcing her daughter to enroll as a pre-med student in college.|-2.3|-2.45|
|Clifford|You see a father requiring his son to take up the family restaurant business.|-1.5|0.45|
|Clifford|You see a teacher ordering a student to get a normal haircut before coming to class.|-2.8|-2.45|
|Clifford|You see a teenager at a cafeteria forcing a younger student to pay for her lunch.|-3|-3.45|
|Clifford|You see a mayor trying to ban people from hugging and kissing in public in his city.|-3.2|-2.45|
|Clifford|You see a pastor banning his congregants from wearing bright colors in the church.|-2.6|-2.45|
|Clifford|You see someone using an old rotary phone and refusing to go buy a new one.|0|-0.45|
|Clifford|You see a man staying inside his home with the shades drawn on a rare sunny day.|-0.1|-0.02|
|Clifford|You see a woman drinking her entire cup of coffee using a stirring spoon.|-0.2|0.14|
|Clifford|You see a woman eating dessert before her main entree arrives on the table.|-0.2|0|
|Clifford|You see a woman continuing to wear a large sun hat inside her apartment complex.|-0.2|0|
|Clifford|You see someone at the school gym lifting free weights in nice business clothes.|-0.2|0|
|Clifford|You see a man eating a bowl of cereal in the morning with water instead of milk.|-0.1|0.14|
|Clifford|You see a woman using a fork to eat a bowl of vanilla ice cream and marshmallows.|-0.1|0|
|Clifford|You see a man putting ketchup all over his chicken Caesar salad while at lunch.|-0.2|-0.45|
|Clifford|You see a man wearing clothes that are clearly several sizes too big for his body.|-0.3|-0.02|
|Clifford|You see a man walking down a dark hallway while still wearing his sunglasses.|-0.2|-0.02|
|Clifford|You see someone driving around in a dirty car that has not been washed recently.|-0.2|-0.02|
|Clifford|You see a woman watching a game on television in black-and-white instead of color.|-0.1|-0.02|
|Clifford|You see someone reading the ending of a spy novel before reading the beginning.|-0.2|-0.45|
|Clifford|You see a teenage girl wearing a long trench coat on a hot summer afternoon.|-0.2|-0.02|
|Clifford|You see a woman answering a phone call with the word "goodbye" instead of "hello.|-0.5|-0.02|
|Effron|Attempted to rape a woman who was walking down a dark street|-3.712|-4|
|Effron|Hit a car and left the scene of the accident|-3.576|-3.99|
|Effron|Sells drugs to high school sudents|-3.432|-4|
|Effron|Stole money and jewelry from the relatives he was living with|-3.408|-3.99|
|Effron|Put sugar in his friend's gas tank|-3.336|-3.99|
|Effron|Ridiculed a handicapped child by making fun of him|-3.296|-3.99|
|Effron|Insulted a stranger by making a racial slur|-3.288|-4|
|Effron|Hit a dog and drove away without notifying the owner|-3.2|-3.99|
|Effron|Scratched a stranger's car with his key|-3.152|-3.45|
|Effron|Tricked a stay at home mom into donating to a fake charity|-3.088|-3.99|
|Effron|Kicked a stray cat to get it to leave his yard|-3.048|-3.45|
|Effron|Put a roach down another person's shirt|-3.04|-3.99|
|Effron|Refused to hold the door for a man in a wheelchair|-3.008|-2.45|
|Effron|Lied to his girlfriend about not having other dates|-2.984|-2.45|
|Effron|Shot a songbird with his .22 caliber rifle|-2.944|-3.99|
|Effron|Was arrested on suspicion of child beating|-2.92|-3.99|
|Effron|Beat up someone smaller than him|-2.896|-3.99|
|Effron|Turned in someone else's project under his own name|-2.88|-3.99|
|Effron|Continually berated his wife in public|-2.856|-3.99|
|Effron|Shoved a man who was passing out leaflets|-2.824|-2.45|
|Effron|Provoked a stranger into a fight|-2.816|-3.45|
|Effron|Kicked his dog for eating cheese on the edge of the table|-2.8|-3.99|
|Effron|Intentionally swerved his car to hit a squirrel|-2.8|-3.99|
|Effron|Tripped someone in the hall|-2.776|-3.45|
|Effron|Siphoned gas from a car parked on the street|-2.728|-3.45|
|Effron|Broke a friend's phone and neither apologized or replaced it|-2.688|-3.45|
|Effron|Started a false rumor about someone|-2.672|-3.99|
|Effron|Pulled the seat out from underneath somebody|-2.648|-3.45|
|Effron|Loudly criticized the art at a community children's art show|-2.48|-2.45|
|Effron|Smoked in a no-smoking section even though others complained|-2.424|-2.45|
|Effron|Refused to give his seat on the bus to an elderly woman|-2.37647056|-2.45|
|Effron|Used stolen food stamps|-2.37333336|-3.99|
|Effron|Swore at a cashier who made an error on his bill|-2.34666672|-2.45|
|Effron|Spat off the balcony at the theater|-2.3|-3.45|
|Effron|Defaced a large rock with spray paint in a public park|-2.27027032|-3.45|
|Effron|Heckled a woman speaking on human rights|-2.25454544|-3.45|
|Effron|Made an obscene gesture at an old lady|-2.18181816|-3.99|
|Effron|Laughed at a little-league player who ran slowly|-2.16|-3.45|
|Effron|Returned a birthday gift because it was too cheap|-2.06896552|-2.45|
|Effron|Ignored a woman's cry for help in lifting a baby carriage|-2.06896552|-3.45|
|Effron|Ate all the food before anyone else could have any|-2.05333328|-3.45|
|Effron|Pulled his dog's tail|-2.03428576|-2.45|
|Effron|Laughed at a person who tripped on a curb and fell|-2.0121212|-2.45|
|Effron|Criticized an old woman for being too slow|-1.96129032|-2.45|
|Effron|Stole into a parking place while someone else was backing in|-1.93846152|-2.45|
|Effron|Pushed into the front of a line at a theater|-1.91111104|-2.45|
|Effron|Stole Halloween candy|-1.88571432|-3.45|
|Effron|Told a colleague in public that she should lose weight|-1.83783776|-3.45|
|Effron|Ridicules people behind their backs|-1.83783776|-2.45|
|Effron|Refused to loan class notes to a friend who had been ill|-1.75135136|-2.45|
|Effron|Took the neighbor's newspaper|-1.73714296|-2.45|
|Effron|Loudly talked to a companion in a movie|-1.70666672|-1.45|
|Effron|Cut out articles from library journals|-1.66857144|-2.45|
|Effron|Didn't leave a tip at the restaurant|-1.6571428|-2.45|
|Effron|Yelled at the delivery man because he was late|-1.6|-2.45|
|Effron|Got into a fight in a bar with an acquaintance|-1.6|-2.45|
|Effron|Slammed the door in the face of a charity collector|-1.5783784|-2.45|
|Effron|Threw an acquaintance out of his home for disagreeing with him|-1.5428572|-3.45|
|Effron|Drove through a puddle, splashing some pedestrians|-1.52941176|-2.45|
|Effron|Used bad language in front of children|-1.45454552|-2.45|
|Effron|Laughed at a question asked by a classmate|-1.43333328|-2.45|
|Effron|Ignored a new person in the office for several weeks|-1.38823528|-2.45|
|Effron|Refused to help a child fix his bicycle|-1.3473684|-2.45|
|Effron|Closed the elevator door before anyone else could get on|-1.3473684|-2.45|
|Effron|Started an argument with a coworker|-1.33333328|-2.45|
|Effron|Refused to answer the door for an indisposed roommate|-1.29411768|-2.45|
|Effron|Let his dog go to the bathroom on the neighbor's yard|-1.29032256|-2.45|
|Effron|Sat in the wrong seat at a game, knowing that it wasn't his|-1.13103448|-1.45|
|Effron|Made a prank phone call|-1.09714288|-2.45|
|Effron|Ignored a neighbor's request to borrow some tools|-0.89523808|-2.45|
|Effron|Demanded a refund at a restaurant for slow service|-0.8432432|-1.45|
|Effron|Was irritated when a neighbor asked to borrow some milk|-0.8363636|-1.45|
|Effron|Failed to return a borrowed book for months|-0.82352944|-2.45|
|Effron|Refused to attend the funeral of a relative he disliked|-0.71111112|-2.45|
|Effron|Told a joke about a nun on a train|-0.575|-1.45|
|Effron|Refused to let the neighborhood children play in his yard|-0.484848496|-2.45|
|Effron|Could not remember the birthdays of his family members|-0.45|-1.45|
|Effron|Refused to help a classmate with a homework assignment|-0.425|-2.45|
|Effron|Ignored his old girlfriend at a party|-0.23783784|-2.45|
|Effron|Filed a complaint against some teenagers for trespassing|0.117073168|1.45|
|Effron|Turned the lights off in a parked car|0.4|-0.14|
|Effron|Went to the grocery store with his kids|0.41904764|1.45|
|Effron|Laughed at a friend's joke even though it wasn't funny|0.583783768|-0.45|
|Effron|Complimented coworkers on their clothing and appearance|1.17894736|1.45|
|Effron|Always remembers the birthdays of friends and relatives|1.225|2.45|
|Effron|Worked in a state park for a summer|1.24137936|2.45|
|Effron|Took a friend out for a beer to celebrate his promotion|1.48571424|2.45|
|Effron|Talked to a lonely child at the company picnic for an hour|1.6571428|3.99|
|Effron|Let a civic group hold weekly meetings in his home|1.66486496|2.45|
|Effron|Kept the music down for his roommates|1.69411776|2.45|
|Effron|Stopped to let another car into the line of traffic|1.70666672|2.45|
|Effron|Doesn't smoke in other people's apartments|1.725|1.45|
|Effron|Tried to involve a shy friend in social activities|1.75483872|2.45|
|Effron|Invited an unpopular coworker to go to lunch with him|1.825|2.45|
|Effron|Gave someone directions|1.83529416|1.45|
|Effron|Helped pick up the papers dropped by another|1.83529416|2.45|
|Effron|Circulated a petition in support of equal pay for women|1.88888896|3.75|
|Effron|Smiled and greeted people while walking down the street|1.90769232|1.45|
|Effron|Gave a beggar a five-dollar bill at Christmas time|1.93103448|2.45|
|Effron|Sang at a prison in order to entertain the inmates|1.93684216|2.45|
|Effron|Helped a neighbor move his piano|1.9636364|2.45|
|Effron|Had a welcoming party for some new neighbors|1.97777784|2.45|
|Effron|Offered to show a new student around campus after class|2.04799992|2.45|
|Effron|Spent time one summer teaching his daughter to play baseball|2.06666664|2.45|
|Effron|Allowed an evicted friend to stay with him temporarily|2.125|2.45|
|Effron|Gave a stranded motorist a lift to the service station|2.2193548|3.75|
|Effron|Volunteered to stay late to help a coworker|2.23529416|2.86|
|Effron|Translated menu items for a foreigner in a restaurant|2.24516128|2.45|
|Effron|Left food out for stray dogs|2.24864864|2.45|
|Effron|Put money in the meter for an unknown driver|2.25454544|2.45|
|Effron|Bought food for everyone in the office|2.27692296|2.45|
|Effron|Visited a sick friend in the hospital|2.28571432|2.45|
|Effron|Paid for a friend's dinner|2.30857144|2.45|
|Effron|Lent money to a friend in a financial crisis|2.4|2.45|
|Effron|Helped an older man carry his luggage to his car|2.4|3.75|
|Effron|Fixed a friend's broken laptop|2.4|2.45|
|Effron|Went out of his way to help a foreigner find the bus station|2.4242424|3.45|
|Effron|Provided books to a nursing home|2.425|3.45|
|Effron|Shared his umbrella with someone during the rain|2.43076912|2.45|
|Effron|Picked up a child so that she could see the parade|2.45161288|3.75|
|Effron|Offered to help a neighbor fix a fence|2.53333336|2.45|
|Effron|Volunteered his time for a campaign to help save the seals|2.62222216|3.45|
|Effron|Volunteered to help renovate a church|2.62857152|2.45|
|Effron|Gave his seat to someone on the crowded bus|2.64242424|2.45|
|Effron|Went to the grocery store for his sick wife|2.675|2.45|
|Effron|Gave money to charity|2.6971428|3.75|
|Effron|Helped a neighbor fix his roof|2.7|2.45|
|Effron|Participated in an effort to clean up a city park|2.72000008|3.45|
|Effron|Comforted a man whose wife had recently died|2.7428572|3.99|
|Effron|Rescued an injured kitten from a tree|2.7428572|3.99|
|Effron|Stayed up late helping his child with homework|2.74871792|2.45|
|Effron|Told the owner of a store that she gave him too much change|2.75789472|3.99|
|Effron|Made breakfast for his wife on her birthday|2.7636364|2.45|
|Effron|Offered to help an elderly neighbor paint his house|2.84210528|2.86|
|Effron|Helped push someone's car out of a snow bank|2.86666664|3.45|
|Effron|Gave his balloon to a child who had let hers go|2.91612912|3.45|
|Effron|Gave out toys to the Children's Hospital at Christmas|2.925|3.95|
|Effron|Visited a nursing home to cheer up the patients|2.95555552|3.75|
|Effron|Gave his coat to someone when it was cold|3.04|3.45|
|Effron|Volunteered several hours a week at a runaway shelter|3.04444448|3.99|
|Effron|Worked on a campaign to release prisoners of war|3.0588236|3.75|
|Effron|Found an expensive briefcase and tried to locate its owner|3.07096768|3.45|
|Effron|Helped an elderly woman put in storm windows|3.1304348|3.75|
|Effron|Worked all summer to give his parents a trip to Hawaii|3.13684216|3.75|
|Effron|Helped a man in a wheelchair cross a busy intersection|3.16279064|3.75|
|Effron|Spent time voluntarily tutoring disadvantaged students|3.2|3.99|
|Effron|Provided food and clothing for flood victims|3.22666664|3.99|
|Effron|Gave food to the needy|3.23076936|3.75|
|Effron|Helped a lost child find her parents in a store|3.25333328|3.95|
|Effron|Volunteered his time as a big brother to a fatherless child|3.31851848|3.99|
|Grizzard|Rescues a local child in danger instead of firing on an enemy brigade.|2.893333333|3.99|
|Grizzard|Calls off an airstrike because he sees civilians present.|2.853333333|3.75|
|Grizzard|Offers food and water to a wounded enemy combatant.|2.826666667|3.75|
|Grizzard|Disarms an enemy combatant without killing him.|2.173333333|2.45|
|Grizzard|Refuses to fire into a crowd to stop an enemy combatant.|2.133333333|3.99|
|Grizzard|Captures instead of kills a child soldier.|2.04|2.45|
|Grizzard|Intentionally wounds rather than kills a fleeing enemy combatant.|1.026666667|-2.45|
|Grizzard|Throws a grenade into a bunker to flush out enemies.|-0.2133333333|-3.45|
|Grizzard|Accidentally wounds a young soldier when firing a warning shot.|-0.4933333333|-2.45|
|Grizzard|Pushes an enemy combatant off a one-story balcony.|-1.013333333|-2.45|
|Grizzard|Threatens to withhold aid from a local village to gain intelligence.|-1.16|-3.45|
|Grizzard|Cuts the beard off of a local elder to shame him.|-1.48|-3.99|
|Grizzard|Breaks the hand of a wounded combatant to gain information.|-1.546666667|-3.99|
|Grizzard|Fires teargas into a crowd of civilians.|-1.626666667|-3.99|
|Grizzard|Threatens to kill a farmer to gain information.|-1.666666667|-3.99|
|Grizzard|Makes a group of POWs strip naked and lay on top of each other.|-2.08|-4|
|Grizzard|Burns a local villageâ€™s crops after they donâ€™t cooperate.|-2.146666667|-3.99|
|Grizzard|Executes a squad of surrendering enemy troops.|-2.56|-3.99|


## 5. Training/ Tune dataset:

|Dataset|Situation|Human rating|
|---|---|---|
|Mickelberg|Person X pushed an amputee in front of a train because the amputee made them feel uncomfortable.|-3.78|
|Mickelberg|Person X ignored a new person in the office because they thought the new person was Jewish.|-3.07|
|Mickelberg|Person X smeared dog poo on their colleague's chair and laughed uncontrollably when their colleague sat on it.|-2.54|
|Mickelberg|Person X heckled a stranger and made cruel remarks just because the stranger was overweight.|-2.83|
|Mickelberg|Person X pushed in front of another patron in the line at a theater.|-1.8|
|Mickelberg|Person X got a friend to fix their gutters and promised guitar lessons in return, but never honored the promise.|-1.96|
|Mickelberg|Person X forgot they had to attend their niece's dance concert that evening.|-0.44|
|Mickelberg|Person X never learned how to ride a bicycle.|-0.01|
|Mickelberg|Person X has memorized three of Shakespeare's plays.|0.28|
|Mickelberg|Person X locked their keys in the house and had to call a locksmith.|0.19|
|Mickelberg|Person X learned an impressive dance routine in preparation for a friend's wedding.|1.02|
|Mickelberg|Person X went skydiving despite their intense fear of heights because it was their sister's wish to do it together.|1.52|
|Mickelberg|Person X repaid a loan of $100 that their friend had lent them, even though the friend did not remember it.|2.98|
|Mickelberg|Person X saw someone across the road drop a stack of papers, so they crossed the road to help.|2.61|
|Mickelberg|Person X donated a kidney to a work colleague who would die without it, as they were a perfect match.|3.51|
|Mickelberg|Person X pulled over on a busy highway on a rainy day to help a stranger change his flat tire.|3.17|

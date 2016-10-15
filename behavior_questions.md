# Behavior Questions

| Common Questions | Newton | RunRecipe | KNN | Finanial |
| -- | -- | -- | -- | -- |
| Most Challenging | Positiven or Negative (Context, sentence, how many po words & negative words, very * 2, dramatically * 2) | Get real-time data from API(call every second, froze account, summary page) | Normalize values to become numeric (weight accordingly, adjust through cross validation) | Several people create funds or end transition day at the same time (Synchronized Methods) |
| What you learnt | API not good for machine learning (Different data sets have their own characteristics) | Adjust Solution based on API features | Adjust attributes to get ideal result | ensure ACID in transactions |
| Most Interesting | IBM API | call Fitbit API | Adjust weight value to improve correctness | Testing,several people click at the same time |
| Hardest Bug | Key-Terms | call Fitbit API | low cross validation rate initially | Several people click at the same time |
| Enjoy Most | real-time analysis, correct conclusion, judges were impressed  | use my own app to run and get fitness summary | get 92% cross validation rate | Testing |
| Conflicts with Teammates | Team management(Asana) | Did little and no communication. Had a talk and split work more in detail | Wanna do same work, list strength and experience, split work in small componenets, rank the first three, coordinate each person has their favor work to do | do little, he was sick, we had to cover his work, we are a team, we need to handle this kind of situation |


![](Screen Shot 2016-10-11 at 10.15.46 AM.png)

During this summer, I worked with a local Consulting Company to develop a "Smart Survey" web platform for them. As you know, normal survey contains few data value since survey takers just want to finish it as soon as possible, and taking survey is not fun at all.

For our platform, we have user-end and consultant-end. For users when they are taking surveys, we tried to do gamification on the user interface, we have a progress bar keeps going up if they type more words for a question, also, we keeps showing hints of "how many people they beat" in the site, which encourages them to type more words.

After we collect enough data, we tried to use NLP for analyzing the survey. We generate key terms by calculating TF-IDF scores, also we have our own algorithms to define whether the key term is positive or negative. For example "negative salary" may indicate that the user is not satisfied with his salary now. This saves great time for the consultants because they do not need to read the whole survey to get the idea, we will provide the information to them. We also utilized IBM watson api to do tone and emotion analysis for the consultants. Our client is impressed by our work and they are using the platform now.

That's the project that I am proud of!
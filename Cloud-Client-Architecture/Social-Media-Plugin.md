---
title: Social Media Plugin
parent: Cloud Client Architecture
---
# Social Media Plugin

Users have interactions with an organization outside of the typical interactions through media like Native Mobile Applications or Web Applications.  Social Media outlets such as Twitter and Facebook, or internal social platforms such as Slack are important forms of interaction that should be part of an overall communication strategy with internal and external users.  

**How do you attract and interact with users outside of custom applications?**

Users aren’t always where you want them to be. They won’t always go to your website or download your application.  However, social media is pervasive. Your users are already there. What’s more, social media tends to be where users ask questions that are perhaps relevant to your company.

The explosion of social media is related to the fact that most of people now use a mobile device as their primary means of accessing application functionality. This encourages responding quickly to notifications, of which social media apps generate a plethora.  What is more, chat platforms of various types tend to be the predominant application type most in use on these devices . Unfortunately, which platform predominates depends on location, culture, and a variety of other reasons that lead to a proliferation of platforms if you want to have reach across geographies, ages and other demographic factors.  The platform that could help you reach your preferred target market could range from WeChat in the Chinese market, to Facebook in the U.S. market (at least for the over-30 age range – for younger users it could be Discord). For the enterprise market, you may be most concerned with reaching your users on platforms like Microsfot Teams or Slack.

What often happens is that people look for help when they are stuck with application issues on social media sites; this could be something like Slack, Facebook or Twitter, or perhaps a more specialized site like LinkedIn. The key here is that humans trust other humans to give them advice - often more so than they would trust the very same information if it were found on a website.

Therefore,

**To reach users in the platforms where they spend the most time, build Social Media Plugins that use the API of the social media application to parse and create posts, DM’s and other artifacts of social media.**

A Social Media Plugin is often (in fact, usually) paired with a ChatBot that can parse natural language text and formulate responses in natural language.  This is especially true of situations where we want to automate or semi-automate the process of responding to messages (such as Tweets) raising complaints or questions about a product or service.  This architecture is shown in Figure 12: Social Media Plugin Architecture below.
 
Figure 12: Social Media Plugin Architecture

One of the key aspects of a successful Social Media Plugin is that the representation of the User should be carried over from the Social Media Plugin into other Interaction Models that the user interacts with.  Thus, if a user asks for help on social media with a task, the results of actions taken through social media should be available on the platform on which they may have originally tried the task, be that a Native Mobile Application, a Web Application, or a Single Page Application.  This is yet another reason to tie the different interaction models together not only through common back-end domain representations like a common user model, but also through a common Event Backbone that can signal these changes to interested parties.

* * *

A Social Media Plugin could be implemented with Dynamic Hook Points [Acherkan] to override specific behavior depending upon the social media context. This can even be user or client specific.

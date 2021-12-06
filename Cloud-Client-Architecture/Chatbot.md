---
title: Chatbot
parent: Cloud Client Architecture
---
# Chatbot

Technologies like a Single Page Application or Native Mobile Application (or any traditional page-based GUI) lends themselves well to a finite set of actions arranged as a common progression.  What happens when the starting place is essentially undefined and the progression unpredictable?  

**How do you help a user navigate in order to perform an action or find data if they are not sure what they’re interested in?**

In many types of applications, such as customer support, it is often hard to build a web site or application that naturally allows people to go directly to the specific piece of information that they need. Users resist navigating deep hierarchies of static pages, and FAQs become unwieldly when there are more than a few dozen entries. Search tools like Google can alleviate this somewhat, but that depends on both the information developer and the user seeing eye-to-eye about the phrasing of keywords and other aspects of search engine optimization. 

What is needed is some way to meet these users where they are - to give them an interaction that either feels like interacting with a human, or that may be actually interacting with a human, intermediated through a program that may first organize the category of help and other prerequisites that a human requires to solve their problem efficiently.

Therefore,

**Communicate with users using their own Natural Language.  Build a chatbot as a service that can be plugged into different web sites, mobile applications and social media platforms.**

Chatbots are not a new form of technology - in a sense they can be traced back all the way to the Eliza program written by Joseph Weizenbaum in 1966. However, recent improvements in Natural Language Processing have made it easier and more efficient to build them than before.  Most chatbots share a common set of architectural features that allow them to be built easily from existing open-source libraries or commercial web-based API’s.  Therefore, they can be implemented as microservices that can be called from within mobile apps, web apps, chat applications (such as Slack or Discord) and social media platforms.  An example of how a Chatbot would be invoked (or embedded within) one or more other types of Interaction Models, along with the relationship between the Chatbot and other patterns is shown below in Figure 13: Chatbot Architecture:
 
Figure 13: Chatbot Architecture

An important aspect of a Chatbot that is different than many of the other Interaction Models we have seen is that a chatbot can help the user navigate amongst through a decision tree of choices.  Rather than a window with fields for name, address, and phone, the chatbot can ask questions of the user interactively: What is your name? What is your Address? What is your phone number?  If the information has already been provided, it can simply skip the question, or ask the questions in different orders. 

The Chatbot itself must take advantage of a set of Natural Language Processing Services that typically parse incoming text and then extract the “intent” (e.g., the relevant domain concept in terms of predetermined entities and actions) from the incoming text.  Likewise, the Chatbot will then either directly or through the intermediation of the Natural Language Processing Services call one or more Domain Services to perform queries whose results are then formatted by the Natural Language Processing Services as output text, or to perform some set of actions based on the user’s intent.  This sort of typical Chatbot architecture is shown below in Figure 14: Chatbot Interactions:
 
Figure 14: Chatbot Interactions

For instance, for simple cases, the open-source Chatterbot library is a machine-learning based conversational dialog engine for Python.  It allows you to build or customize logic adaptors that take in preprocessed statements from the user and either provide you the best match to a response, or invoke other adaptors for more specific domain types (like date/time or math).  The system learns from a set of provided example statements in order to determine the best response.

The system that brought Chatbots back into common use, and still one of the most sophisticated, was the IBM Watson natural language engine, derived from the research system that won the game show Jeopardy! against top human competitors in 2011.  This has now evolved into the Watson Assistant suite of services, that work from a set of provided Intents (which are goals learned from multiple examples) in order to understand how to respond to a particular statement.  Likewise in Watson, you can define specific Entities that are found in the conversation, and even specify a conversational flow for a complex interaction that includes slots to hold the different entities you identify (such as the time for a dinner reservation).  Actions are the tasks that the system undertakes on a user’s behalf (such as searching for information as in what time tables are open at the restaurant). 

Somewhere in between the two ends lie the Amazon Lex service, which is connected to the suite of services that includes the Alexa voice service.  It also allows you to define Bots built up from Intents derived from samples, but fulfills each matched intent with a custom function built on AWS Lambda.

* * *

An important consideration in building a Chatbot is that you have to consider that it is a user interface channel into an Enterprise application much like any other user interface choice. That means you have to plan for connecting requests from your chatbot into the back-end API's that your system presents, although due to the conversational nature of the interaction, these API's often end up being heavily mediated to strip down large amounts of data into smaller answers more uniquely suited to the nature of chat. That means that patterns like Backend for Frontend become even more important as you consider chatbots as part of a front-end architecture.

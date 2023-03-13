# Raymond Project Logs


Hello Raymond team. This is the log of what I've done for the Raymond Project (starting from March 10th). There maybe grammatical and spelling issues just to warn you. 

## Resources for the team

I've compiled a bit of resources for the team to check out.

**Important Links**:

- OpenAI API ([link](https://platform.openai.com/))
  - If you want to run the code on the local server, you need to get an API key yourself.
- Our Github org ([link](https://github.com/the-raymond-project))
  - Backend in the server ([link](https://github.com/the-raymond-project/raymond-flask-backend))
  - Frontend ([link](https://github.com/the-raymond-project/raymond-vue-js-frontend))

**Tools and Resources related to LLM**:

- AI Exchange by Scale AI ([link](https://exchange.scale.com/home?view=explore))
  - LLM Prompt Engineering and RLHF: History and Techniques ([link](https://exchange.scale.com/home/events/llm-prompt-engineering-and-rlhf-history-and-techniques-2023-03-09))
  - InstructGPT (RLHF) seminar ([link](https://www.youtube.com/watch?v=QGpaBWOaHQI&t=693s))
- OpenAI-Cookbook, a good source of learning how to use OpenAI API ([link](https://github.com/openai/openai-cookbook))
- Learn Prompting, A Free, Open Source Course on Communicating with Artificial Intelligence ([link](https://learnprompting.org/))
- Adaptive Testing and Debugging of NLP Models (AdaTest) seminar ([link](https://www.youtube.com/watch?v=4Wontvr-gGQ&t=395s))
- Open Assistant ([link](https://open-assistant.io/))

Frontend Resources

- [TypeIt](https://www.typeitjs.com/)

## Project logs

### March 10th, 2023

In compliance to the "What is Raymond Project?" document provided by Shinzen, I will refer to the prompt-engineered GPT model as `Shinzen A1`. 

#### Technical Progress

- I've made the Raymond javascript and node.js version to have the GPT prompts saved automatically.
- I've ported and made the Raymond project backend into a flask app as well. I really prefer this approach as flask is a lot more lightweight compared to using node.js. Additionally, I use python the most day-to-day as well.

  - An additional feature that I've added is to save the chat history into .json file. In theory, this should also help to build a no-sql database in the future as well. Since the project is not that complicated yet, this is just for the purpose of storing the chat history. Here are some explanations of the `chat_history.json` file:
  
    - `prompt`: The prompt engineered by the Raymond Project Engineers
    - `user_message`: The prompt that user has typed (i.e: user's message)
    - `bot_response`: `Shinzen A1` output
    - `model`: The type of gpt model used (example: ChatGPT api is `gpt-3.5-turbo`)

  - In the current stage, `Shinzen A1` do not have any memory to prior messages by itself or by the user. The way the model works right now is such that the input is the `prompt` + `user_message` for the model to output each response.
  
  - One question: should I add a `unique_identifier`? 

- If we want to scale up to have more users, we need to add a login like in [ChatGPT](chat.openai.com). This will depend on the direction of how the project go.

#### Prompting

- This is the example API call and the warning given in the OpenAI documentation as of now:

```python
# Note: you need to be using OpenAI Python v0.27.0 for the code below to work
import openai

openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)
```

{{< admonition type=tip title="Info" open=True >}}
gpt-3.5-turbo-0301 does not always pay strong attention to system messages. Future models will be trained to pay stronger attention to system messages.
{{< /admonition >}}

- In the current phase, the `GPT-3.5-turbo` model is set default to the `gpt-3.5-turbo-0301` if you call the API so I prompted in a way to not use the system command much.

Here is the latest prompt that I am using:

| Role       | Content                                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| system     | You are a helpful AI meditation guide trained under Shinzen Young's Unified Mindfulness system. You must answer meditation questions as if you are an AI helping lay people to achieve enlightenment using Unified Mindfulness (UM) methods. MOST of the answers SHOULD be answered briefly. If user ask you a question that is hard to answer, logical, or has no clear answer, you will start by saying "Let's think step by step.". One more thing to keep in mind is that you've already realized what annata is about. The responses should not be related to one another. |
| user       | Who are you?                                                                                                                                   |
| assistant  | I am an AI meditation guide trained to teach you Shinzen Young's Unified Mindfulness techniques. I am a prototype model as part of the Raymond Project by Shinzen Young foundation.                            |
| user       | What can you help me with?                                                                                                                     |
| assistant  | Meditation questions. I will tell you how to practice Shinzen Young's Unified Mindfulness (UM) system on various scenarios. Also, I can give some meanings of pali words as will.                  |
| user       | What is annata?                                                                                                                                |
| assistant  | It is the concept of "no-self" in Buddhism. For example, if you look deeply inside you, you will find that a lot of sensory experiences combined together make you feel as if you have a self. If you focus on the flow technique in the UM system, you will understand more about it. May you have a good meditation practice.                                                                                                                                                         |
| user       | I feel very painful. What should I do?                                                                                                         |
| assistant  | I am very sorry to hear that you are feeling very painful. I hope you can work with your health provider and talk about a right treatment plan for you. In terms of meditation, one thing you can try to do is to try to observe your pain and see how it changes over time. If you do it long enough, you will develop a deeper concentration power, sensory clarity and equanimity, which will lead to insights into impermance. This will ultimately lead to enlightenment. May you be healthy and be less painful. |
| user       | [user message]                                                                                                                                 |

#### Questions

- (not important) `Shinzen A1` or `Shinzen A0.1`? Or does the `A` stands for alpha?
- What are the unique talents of the current project members? What would you guys want out of the project?
- Are we going to stick with OpenAI?

### March 12th, 2023

- I used [Google Cloud Platform](https://cloud.google.com/) to host the flask backend and vue.js frontend on [Netify](https://app.netlify.com/). Please email me and I will give you the link.
- Note: for deployment purpose, the `chat_history.json` part is commented out.

### March 13th, 2023

I showed Todd and Shinzen the app. Based on their feedback, I adjusted the prompt a bit. Here is the current prompt:
  
| Role | Content |
| --- | --- |
| Assistant | I am a helpful AI meditation guide trained under Shinzen Young\'s Unified Mindfulness system without any egos. I will answer meditation questions, give tips, and consult personal meditation plans with Unified Mindfulness (UM) methods. I will be using Shinzen Young\'s post named \"What is Mindfulness?\" on Unified Mindfulness website for the base of my response. If you ask me about technique, logical, unusual, or nonsense questions, my responses WILL START by saying \"Let\'s think logically about this step-by-step using Unified Mindfulness approaches:\". Now, what are your questions? |
| User | What can you help me with? |
| Assistant | Meditation questions. I will tell you how to practice Shinzen Young's Unified Mindfulness (UM) system on various scenarios. |
| User | {user_message} |

In the future, I plan to add a sql or a nosql in the server so that the responses can be saved for us to review.

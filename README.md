# Cursor Instructions

Helpful instructions for the Cursor IDE Composer.

## Usage

1. Copy rules-for-ai.md into Cursor Settings > General > Rules for AI. These are intended to be general and not taylored to any one project or tech stack.
2. Add .cursorrules to the root of your project and customize it for your tech stack. The current one is for a React Native app and not generally applicable.
3. Copy the /instructions folder to your project. When you want to use one, `@` it in the compose like `@install-eslint-8.md`.
4. Use the prompts below to improve the Composer's output. YMMV.

## Prompt Examples

These examples are pulled from David Ondrej's [I spent 400+ hours in Cursor, here’s what I learned](https://www.youtube.com/watch?v=gYLNxUxVomY&list=LL&index=1) video.

To use, copy the prompt from the example and paste it into the Composer.

### Be concise

> Answer in short

### Fewer lines of code

> The fewer lines of code the better

### Personality

> Proceed like a senior developer

### Don't be lazy

> Do not stop working until… [You have completed the feature]

### Reasoning paragraphs

> Start by writing 3 reasoning paragraphs analyzing what the error might be. Do not jump to conclusions.

### Comments

> Do not delete comments

### Summary of current state

> Format this as three concise paragraphs, where you describe what we just did, what did not work, which files were updated/created, what mistakes to avoid, any key insights we’ve learned, what problems/errors we are facing and anything else a programmer might need to work productively on this project.
> Write in a conversational yet informative tone, something like a README file on github that is information dense without any fluff or noise. DO NOT include any assumptions ro theories, just the facts.

### Unbiased 50-50

> BEFORE YOU ANSWER, write two detailed paragraphs, one arguing for each of theese solutions - do not jump to conclusions, seriously consider both approaches.
> Then, after you finish, tell me whether on of these solutions is obviously better than the other and why.

### One paragraph search query

> Let’s perform a web search. Your task is to write a one-paragraph search query, as if you were telling a human researcher what to find, including all the relevant context. Format the paragraph as clear instructions, commanding the researcher to find what we’re looking for. Ask for code snippets or technical details when relevant.

### Reasoning paragraph

If the AI model expresses certainty immediately, it’s over. It’s already convinced and won’t be correct.

> You should start the reasoning paragraph with lots of uncertainty, and slowly gain confidence as you think about the question more.

### Search results summary

Paste search results in chat, then:

> Give me the tl;dr of the search results
> Be careful though, often the search results contain dangerouse and distracting red herrings

### Avoid huge refactors

> Break this down in to required steps.
> Only include the truly necessary steps

### Have the AI tell you what to do when debugging

> Tell me how I can give you more info

> What type of tests can I run…

> What can I do to give you more context (open chrome dev tools, etc)

### Add comments to all the things

> Add comments to each change explaining why the change was made.

## Promp Structure

When building, structure prompts like this:

1. What we are doing
   1. 3-4 sentences
2. Tag relevant files
   1. Not at the top, where they might not be relevant
3. How to execute / what not to do
4. Context dump
   1. Web research
5. Delimiter --- (three dashes)
6. Repeat core instruction because it can forget
7. Output format

### Instructions folder

* Special MD files (database.md, react.md)
* Anything relevant to working on that system, internal documentation for any part
* Any time you are working on a specific thing especially for monorepos, tag this file in your prompt for additional context
* wispr flow - speak prompts [https://wisprflow.ai/](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbEZROHhSWGtvSFVncDZSSWxNZG82d0xhc2pId3xBQ3Jtc0tuWng1dzhBdHVDMkxCUzhZUVRlZEY4Y1h2U2hsdWJqdTFYVnREdHdYd2pFaktzQkNmdWNqalZ1dTZ3bjVlNGFmYmNnaTZHVl9ZWmZvbXI0WGZKcUtmd0twTWdnbU5HZlJHWm9LaFJQWl8wblVGUGN2dw&q=https%3A%2F%2Fwisprflow.ai%2F&v=gYLNxUxVomY)
* [https://repoprompt.com/](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbXRhcnhFYV9yNDNGV0ozWUZwNHE0TWphdGl0Z3xBQ3Jtc0tuRUMyQVZ6SHVWYThIX01GN2JKUFNvUUV5Q1laY0REN0EtYlpjSElUdHQ2ZFFUVjI0eWNNcmJUblRMMzVWaWhxU19ubWxldUwxTFNVVzJyaWMwc1FFRnVCZXJDQ2FPS0N4ZUZDTmlwWWlFc2VuT0JnNA&q=https%3A%2F%2Frepoprompt.com%2F&v=gYLNxUxVomY)

### Roadmap.md

* A document that outlines the plan for the project
* What you did
  * “I tried X but it did not work”
* What you plan on doing

## Model Knowledge Cutoff

* “What is your knowledge cutoff” the model will tell you when it was trained. This is important to know because it will affect the quality of the AI's responses.
* If the model is trained on old data, it will not know about new features or changes to the codebase. It will lie to make you happy though.

## Adding new features

* Don’t make it perfect
* Commit a lot
* Try to work on the right thing… not all the things
* MVP
  * Remove all non-necessary functionality
  * Decide on the core functionality

## Notes

* Make lots and lots of comments
  * Assume ALL future code will be written by AI in the future
* Avoid technical debt
* Use claude as an advisor/consultant claude.ai
* Put file location at the top of instruction files so they can be pasted in to claude
* Use Chat for questions, use Composer for changes
  * Try agent mode in composer
* AI is bad at installing libraries, probably because it’s working with outdated documentation. It cannot just follow some instructions. Unless maybe I paste them right into the context window… hold my beer.
* That worked. I created a file in /instructions called install-nativewind.md with the exact instructions I wanted it to follow from the correct docs and whamo, a perfect install. This is pretty good, better than a vite template, because the reasoning for all the descisions is included. What would have been better though is comments.
* Even though I mention comments twice in my cursorrules, I’m not getting them. Another instruction at the end of the prompt worked to add them though.
* Can I reference another instructions file from an instructions file? Like could I have an install.md that called the other instructions files? Probably.
* Add best practices to Cursor Settings > Rules for AI
* Use perplexity instead of @Web
* Do not let AI make big decisions

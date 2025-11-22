Copilot cheat sheet
===================

# Usage

- Place cursor or select text
- Cmd+I open inline chat
- Ask question
- Tab: accept proposal
- Option+] next proposal
- Option+[ previous proposal

Slash
- /explain: provides explaination
- /suggest: code suggestion
- /setupTests
- /tests: generate tests
- /fixTestFailure
- /comment: comment to code
- /fix: propose fix
- /help: copilot reference help
- /optimize selected code
- /generate code to answer a specific question
- /doc add comments to the selected code
- /new generate a new file

Chat participants:
- type @ to get the list of participants
- @github use github specific skills 
- @project when you want Copilot to consider all of the files in your project
- @terminal agent helps you chat with GitHub Copilot to interact with the terminal. .e.g @terminal How do I fix the error message I'm seeing?
- @workspace, which is aware of your entire workspace. It allows you to ask questions about the entire project.
- @file focuses on the content of a specific file
- @directory considers the contents of a specific directory

Scope referencing
- #file: <specific filename>
- #selection <instructions>
- #codebase a bit like @workspace

Chaining example: @workspace /explain #file:toto.java

Used for:
- Code generation
- Debugging assistance: select code and ask a question
- Code explanation

Command line:
- gh copilot <command>
- configure an alias: echo 'eval "$(gh copilot alias -- zsh)"' >> ~/.zshrc

see : https://docs.github.com/en/copilot/how-tos/chat-with-copilot/chat-in-ide

# Prompt

The 4 Ss are the basis for creating effective prompts:
- Single: Always focus your prompt on a single, well-defined task or question
- Specific: Ensure that your instructions are explicit and detailed
- Short: While being specific, keep prompts concise and to the point
- Surround: Utilize descriptive filenames and keep related files open

Context:
- 'Surround' principle. The more contextual information provided, the more fitting 
   the generated code suggestions are. For example, by adding some comments
- Using examples can clarify your requirements and expectations
- Strategic iteration. Your first prompt might not always yield production-ready code, 
  and that's perfectly fine. Rather than spending time manually refining the output, 
  treat it as the beginning of an efficient dialogue with Copilot


# Learning

- Zero-shot learning: relying solely on its foundational training
- One-shot learning: a single example is given, aiding the model in generating more context-aware responses that follow your specific patterns and conventions
- Few-shot learning:  everal examples, which strike a balance between zero-shot unpredictability and the precision of fine-tuning
- Chain prompting and managing chat history: extended conversations. turn 1: "do this" tuen 2: "do that"
  - Summarize context
  - Reset and provide focused context 
  - Use concise references to previous work:
- Role prompting for specialized tasks
  - "Act as a cybersecurity expert. Do ..."
  - "Act as a performance optimization expert. Do .."
  - "Act as a testing specialist. Create ..."

# Prompt Process Flow

## Inbound Flow

- Secure prompt transmission and context gathering
  - Transmission of the prompt
  - Context gathering
    - Code before/after
    - File names and types modified
    - Information about adjacent open tabs
    - Info about project structure and paths
    - Info about programming language + frameworks
    - Fill-in-the-middle technique
  - Translate high-level request into concrete coding task
- Proxy filter: WAF
- Toxicity filter:
  - Hate speech and inappropriate conten
  - PII
- Code Generation with LLM

## Outbound Flow

- Post-processing and resopnse validation
  - Code quality: security checks
  - Matching public code: optionally enabled - do not return too close to public code
- Suggestion delivery
  - Grow knowledge based on accepted suggestions
  - Learn and improve based on accepted/rejected
- Repeat subsequent prompts

# Copilot Data

- Formatting: optimised for optimal presentation
- User engagement: ask follow-up questions, clarifications, additional inputs
- Data retention: retain prompts and context for 28 days

# Prompt types

- Direct questions
- Code related requests
- Open-Ended queries - how can I improve the perf of my python app"
- Contextual prompts

# Limited Context Windows

- 500 lines of code
- 4K tokens context window

# Model

LoRA fine-tuning: But LoRA (Low-Rank Adaptation) fine-tuning is a clever alternative. It's used to make large pretrained language models (LLMs) work better for specific tasks without redoing all the training.
- LoRA adds smaller trainable parts to each layer of the pretrained model, instead of changing everything.
- The original model remains the same, which saves time and resources.

copilot model:
- Standard models (GPT-4o)
  - Simple code generation
  - 1 PRU per request
- Premium models (o1-preview, o1-mini)
  - enhanced reasoning capabilities for complex problems
  - 2 PRUs per request

# Comment Driven code

- Function implementation comment added to a function stub to describe a function to generate the code
- Code completion comment used inline to auto generate a function with implementation
- Variable naming is an inline comment to influence the variable names to be generated
- Algorithm selection structured comment describing the goal expecting copilot to generate the code


# Exercises
- https://github.com/bsbl/skills-getting-started-with-github-copilot/issues/1
- https://github.com/bsbl/skills-build-applications-w-copilot-agent-mode/issues/1


# Resources

- https://codespaces.new/MicrosoftDocs/mslearn-advanced-copilot
- https://code.visualstudio.com/docs/copilot/reference/copilot-vscode-features
- https://docs.github.com/en/copilot
- https://microsoftlearning.github.io/mslearn-github-copilot-dev/Instructions/Labs/LAB_AK_04_develop_unit_tests_xunit.html
- https://docs.github.com/en/copilot/concepts/billing/copilot-requests
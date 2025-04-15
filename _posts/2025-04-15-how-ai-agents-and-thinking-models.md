Curious about how AI agents and thinking models can use multi-step reasoning and an available API to reach a goal? My Google colleague Cody Oss designed [a clever demo](https://github.com/codyoss/helloworld-agent) to challenge a small instance of Gemma 3 running on his laptop. First, he wrote two basic CRUD-type functions in Go: GetEmployee(id string) and ListEmployees(). Then he added an agent loop with a helper function to scan the model's responses for calls to his CRUD functions. That's right, the secret sauce to giving a model the ability to programmatically call tools can be as simple as scanning the model's responses for substrings that look like calls to known tools. Once one is found, Cody's agent loop parses the plaintext, attempts to execute the call on behalf of the tool, and adds the result to the ongoing model prompt.

The really clever thing about Cody's demo is that it asks the agent a question that requires TWO related function calls: ListEmployees only returns employee IDs, which is not sufficient to answer Cody's question. To get the answer, the agent must reason that it needs to follow up by calling GetEmployee repeatedly with each employee ID that it received. Only once it has called GetEmployee for every ID returned by ListEmployees can it answer the question.

Can Gemma 3 on a laptop do it? TL;DR: Yes.

https://github.com/codyoss/helloworld-agent

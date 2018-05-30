## Personality Chat API
Personality Chat API can be called directly in your application or chatbot code. The nuget package provides a wrapper for calling the API. In the API, user query is matched with our scenarios. For successfully matched user queries, a list of scenario responses with score is returned. You can customize this as you want. Pick a persona voice that you want the chat response in.

Example:

	If personality is set to "Professional" 
	User input query to the bot: "so bored!!"
	Matched scenario: "I am bored"
	Response: "Well, let me know if there’s anything I can do for you."
	

#### Console app calling Personality Chat API using Core Package
Include the package [Microsoft.Bot.Builder.PersonalityChat.Core](https://www.nuget.org/packages/Microsoft.Bot.Builder.PersonalityChat.Core/1.0.0-alpha-m1.0)
Initialize `PersonalityChatService` and choose a personality in whose voide the response should be returned. Options include `PersonalityChat.Professional`, `PersonalityChat.Friendly` or `PersonalityChat.Comical`.
Call the PersonalityChat API with `QueryServiceAsync`. It returns a response from the top matched scenario based on the confidence score. If there are multiple valid responses for a single scenario, a random one is chosen.

```csharp
        static void Main(string[] args)
        {
            PersonalityChatOptions PersonalityChatOptions = new PersonalityChatOptions(string.Empty, PersonalityChat.Professional);
            PersonalityChatService PersonalityChatService = new PersonalityChatService(PersonalityChatOptions);

            while (true)
            {
                Console.Write("User: ");
                string userInput = Console.ReadLine();

                if (userInput.ToLower() == "quit")
                {
                    break;
                }

                var PersonalityChatResults = PersonalityChatService.QueryServiceAsync(userInput).Result;

                string botOutput = PersonalityChatResults?.ScenarioList?.FirstOrDefault()?.Responses?.FirstOrDefault() ?? "";
                Console.WriteLine("Bot: " + botOutput);
            }
```

#### Calling rest API
[Rest API details](https://github.com/Microsoft/BotBuilder-PersonalityChat/blob/master/CSharp/Core/Library/PersonalityChatService.cs)
[API request](https://github.com/Microsoft/BotBuilder-PersonalityChat/blob/master/CSharp/Core/Library/PersonalityChatRequest.cs)
[API response](https://github.com/Microsoft/BotBuilder-PersonalityChat/blob/master/CSharp/Core/Library/PersonalityChatResults.cs)
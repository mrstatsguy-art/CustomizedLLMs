import anthropic

ANTHROPIC_API_KEY = "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"

# Initialize the client
client = anthropic.Anthropic(api_key=ANTHROPIC_API_KEY)

def test_model(model_name):
    try:
        print(f"Testing model: {model_name}...")
        message = client.messages.create(
            model=model_name,
            max_tokens=20,
            messages=[{"role": "user", "content": "Say 'Key is working!'"}]
        )
        print(f"Success with {model_name}: {message.content[0].text}\n")
        return True
    except anthropic.NotFoundError:
        print(f"Error: Model '{model_name}' was not found or is restricted for this API key.\n")
        return False
    except Exception as e:
        print(f"An unexpected error occurred: {e}\n")
        return False
test_model("claude-sonnet-5-5")

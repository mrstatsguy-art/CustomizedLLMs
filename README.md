# CustomizedLLMs


import anthropic
ANTHROPIC_API_KEY = 
# Initialize the client (automatically reads ANTHROPIC_API_KEY)
client = anthropic.Anthropic(api_key=ANTHROPIC_API_KEY)

try:
    message = client.messages.create(
        model="claude-opus-5-5",
        #model="claude-3-5-sonnet-20241022",
        max_tokens=20,
        messages=[
            {"role": "user", "content": "Say 'Key is working!'"}
        ]
    )
    print("Success:", message.content[0].text)

except anthropic.AuthenticationError:
    print("Authentication Error: Your API key is invalid or expired.")
except anthropic.PermissionDeniedError:
    print("Permission Error: Your key lacks access to this model or workspace.")
except anthropic.RateLimitError:
    print("Rate Limit / Billing Error: Check your account credits or rate limits.")
except Exception as e:
    print(f"An error occurred: {e}")

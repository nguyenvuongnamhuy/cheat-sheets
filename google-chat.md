# Table of Contents

- [Webhook](#webhook)
  - [Create new webhook](#create-new-webhook)
  - [Schedule messages](#schedule-messages)
  - [Send message](#send-message)
    - [To a space](#to-a-space)
    - [In a thread](#in-a-thread)
    - [With image](#with-image)
    - [Format](#format)
      - [Bold](#bold)
      - [Italic](#italic)
      - [Strikethrough](#strikethrough)
      - [Code](#code)
      - [Link](#link)
      - [Code block](#code-block)
  - [Schedule a message](#schedule-a-message)

# Webhook

## Create new webhook

1. Click to namespace
2. Select Apps & integrations
3. Click Add webhooks
4. Fill webhook information
5. Save
6. Copy webhook url

## Send message

### To a space

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"First message\",
	}"
```

### In a thread

- Add option `REPLY_MESSAGE_FALLBACK_TO_NEW_THREAD` and property `name` in `data.thread`
- Value `THREAD_ID` can get from response after sending message by webhook or can get from on UI (copy thread url)

```bash
curl -X POST 'webhook_url&messageReplyOption=REPLY_MESSAGE_FALLBACK_TO_NEW_THREAD' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"First message\",
		\"thread\": {
			\"name\": \"spaces/${SPACE_ID}/threads/${THREAD_ID}\"
		}
	}"
```

### With image

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"cards\": [
			{
				\"header\": {
					\"title\": \"Example title\"
				},
				\"sections\": [
					{
						\"widgets\": [
							{
								\"image\": {
									\"imageUrl\": \"https://codeskulptor-assets.commondatastorage.googleapis.com/assets_clock_background.png\"
								}
							}
						]
					}
				]
			}
		],
	}"
```

### Format

- Standard Markdown syntax isn't supported for underline, text color, and bullet lists

#### Bold

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"\*bold\*\"
	}"
```

#### Italic

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"\_italic\_\"
	}"
```

#### Strikethrough

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"\~strikethrough\~\"
	}"
```

#### Code

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"\`code\`\"
	}"
```

#### Link

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"text\": \"https://example.com\"
	}"
```

or with alias content

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"cards\": [
			{
				\"sections\": [
					{
						\"widgets\": [
							{
								\"textParagraph\": {
									\"text\": \"<a href=\'https://example.com\'>Click here</a>\"
								}
							}
						]
					}
				]
			}
		]
	}"
```

### Code block

```bash
curl -X POST 'webhook_url' \
	--header 'Content-Type: application/json' \
	--data "{
		\"cards\": [
			{
				\"sections\": [
					{
						\"widgets\": [
							{
								\"textParagraph\": {
									\"text\": \"<pre>Code\nBlock\nMultiple\nLines</pre>\"
								}
							}
						]
					}
				]
			}
		]
	}"
```

## Schedule a message

- Integrate with Google App Scripts

---

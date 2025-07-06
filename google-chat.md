# Table of Contents

- [Webhook](#webhook)
  - [Create new webhook](#create-new-webhook)
  - [Schedule messages](#schedule-messages)
  - [Send message](#send-message)
    - [To a space](#to-a-space)
    - [In a thread](#in-a-thread)
    - [With image](#with-image)
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

## Schedule a message

- Integrate with Google App Scripts

---

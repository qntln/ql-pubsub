# ql-pubsub

This is a fairly simple publish-subscribe system based on asyncio queues. It connects many publishers to many subscribers.

All publishers send namespaced messages to a single hub, which then fans them out to appropriate subscribers.

**This code will be released in November 2016.**

## Hub
```python
hub = pubsub.Hub()
```

## Publisher
```python
publisher1 = pubsub.Publisher(hub, ('some', 'namespace'))
publisher1.publish({'data': 42})
```

## Subscriber
```python
subscriber1 = pubsub.Subscriber(hub, 'subscriber1')
subscriber1.subscribe(('some', '*'))

while True:
    key, payload = await subscriber1.consume()
    print(key)      # ('some', 'namespace')
    print(payload)  # {'data': 42}
```
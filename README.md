# Wellness Message Dispatcher

A Rails application that schedules unique email messages for active subscribers and stops delivery after each subscriber has received the available message set.

## Delivery rules

```text
scheduled job -> active subscribers -> choose not-yet-delivered message
                                   -> email -> record association
                                   -> no remaining message: skip
```

```bash
bundle install
rails db:create db:migrate db:seed
bundle exec rails server
```

Run the configured background worker and scheduler separately, or use the included container setup after reviewing its environment.

The implementation demonstrates deduplication through delivery associations and active-subscriber filtering. It does not establish unbounded scalability. Large lists require database/index review, batching, queue back-pressure, provider rate limits, retries, idempotency, bounce handling, and unsubscribe/compliance controls. Tests exist across models, jobs, and controllers but were not run during review.

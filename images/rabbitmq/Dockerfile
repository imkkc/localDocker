FROM rabbitmq:3.8.14-management
COPY rabbitmq_delayed_message_exchange-3.8.9-0199d11c.ez /plugins
RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
EXPOSE 5672
EXPOSE 15672

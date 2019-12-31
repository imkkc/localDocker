FROM rabbitmq:3.8-management
COPY rabbitmq_delayed_message_exchange-3.8.0.ez /plugins
RUN rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
EXPOSE 5672
EXPOSE 15672

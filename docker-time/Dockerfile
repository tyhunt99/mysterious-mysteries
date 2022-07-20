FROM ubuntu

WORKDIR /app/

COPY . .

RUN apt-get update && apt-get install tzdata

ENV TZ=America/Denver
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ENTRYPOINT [ "./entrypoint.sh" ]

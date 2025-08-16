FROM ruby:3.1-alpine

WORKDIR /app

# Устанавливаем зависимости для сборки гемов
RUN apk add --no-cache build-base libffi-dev

# Копируем Gemfile и Gemfile.lock (если есть)
COPY Gemfile* ./

# Устанавливаем гемы
RUN bundle install

# Копируем остальные файлы приложения
COPY . .

# Запуск приложения
ENTRYPOINT ["ruby", "app.rb"]

FROM ruby:3.1
WORKDIR /app
RUN apk add --no-cache build-base libffi-dev
COPY Gemfile* ./
RUN gem install bundler && bundle install
COPY . .
ENTRYPOINT ["ruby", "app.rb", "-o", "0.0.0.0", "-p", "80"]

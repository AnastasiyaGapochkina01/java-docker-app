FROM ruby:3.1
WORKDIR /app
COPY Gemfile* ./
RUN gem install bundler rackup puma && bundle install
COPY . .
ENTRYPOINT ["ruby", "app.rb", "-o", "0.0.0.0", "-p", "80"]

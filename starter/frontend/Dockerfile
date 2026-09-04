FROM public.ecr.aws/docker/library/node:18.14.2-alpine3.17 AS build

ARG REACT_APP_MOVIE_API_URL
ENV REACT_APP_MOVIE_API_URL=${REACT_APP_MOVIE_API_URL}

WORKDIR /app

# Copy dependdency files
COPY package*.json ./

# Install packages
RUN npm ci

# Copy code
COPY . .

# Build the app
RUN npm run build

FROM public.ecr.aws/docker/library/nginx:1.25-alpine

COPY --from=build /app/build /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
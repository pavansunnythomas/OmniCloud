# Use the full image so C++/Python dependencies can compile
FROM node:22-bookworm AS deps 

WORKDIR /app
COPY backend/package*.json ./
RUN npm install --omit=dev

# Keep the slim image for the actual runtime
FROM node:22-bookworm-slim AS runtime 

WORKDIR /app
ENV NODE_ENV=production

COPY --from=deps /app/node_modules ./node_modules
COPY backend/package*.json ./
COPY backend/src ./src

RUN mkdir -p /app/data

EXPOSE 8787
CMD ["npm", "start"]

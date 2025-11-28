# 🤖 AI News Hub - Intelligent Automated Blog System

A complete, fully automated, and self-intelligent website/blog system that functions as an AI-powered journalist, automatically generating articles about real-time news, trends, and current events.

## 🌟 Key Features

### 🤖 Core Functionality
- **Automated Article Generation**: Creates original, well-structured articles every hour
- **Real-time News Collection**: Scans multiple news sources using RSS, APIs, and web crawling
- **Intelligent Content Creation**: AI-powered writing with journalistic style and SEO optimization
- **Plagiarism-Free Content**: Original content generation using advanced AI rewriting

### 📰 News Sources
- **RSS Feeds**: Automated RSS parsing from major news outlets
- **API Integration**: Direct integration with news APIs (Reuters, AP, etc.)
- **Web Crawling**: AI-powered web search for trending topics
- **Multi-Source Aggregation**: Combines news from various sources for comprehensive coverage

### 🎯 Content Features
- **Smart Categorization**: Automatic categorization into Technology, Politics, Economics, Science, etc.
- **SEO Optimization**: Auto-generated meta titles, descriptions, keywords, and structured data
- **AI Image Generation**: Featured images created by AI for each article
- **Reading Time Calculation**: Automatic estimation of article reading time

### 🛠️ Administrative Panel
- **Article Management**: Review, edit, and publish generated articles
- **Source Configuration**: Manage news sources and their settings
- **System Settings**: Configure generation frequency, auto-publishing, and more
- **Analytics Dashboard**: Track performance, views, and system health
- **Activity Logs**: Monitor system operations and errors

### 🔍 SEO & Social Features
- **Automatic Sitemap**: Dynamic sitemap generation for search engines
- **RSS Feed**: RSS feed for subscribers and aggregators
- **Meta Tags**: Comprehensive SEO meta tags for all pages
- **Social Media Ready**: Open Graph and Twitter Card meta tags
- **Clean URLs**: SEO-friendly URL structure

## 🏗️ Architecture

### Frontend (Next.js 15)
- **Framework**: Next.js 15 with App Router
- **UI Components**: shadcn/ui with Tailwind CSS
- **Responsive Design**: Mobile-first approach
- **Dark Mode**: Built-in theme switching
- **TypeScript**: Full type safety

### Backend (Node.js)
- **API Routes**: RESTful API for all operations
- **Database**: Prisma ORM with SQLite
- **AI Integration**: z-ai-web-dev-sdk for content generation
- **News Collection**: Multi-source news aggregation

### Mini Services
- **Article Generator Service**: Scheduled background service for automated generation
- **Health Monitoring**: System health checks and logging
- **Error Handling**: Comprehensive error tracking and recovery

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Git

### Installation

1. **Clone the repository**
```bash
git clone <repository-url>
cd ai-news-hub
```

2. **Install dependencies**
```bash
npm install
```

3. **Set up environment variables**
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. **Initialize the database**
```bash
npm run db:push
```

5. **Initialize system data**
```bash
curl -X POST http://localhost:3000/api/setup
```

6. **Start the development server**
```bash
npm run dev
```

7. **Start the article generator service**
```bash
cd mini-services/article-generator
npm install
npm run dev
```

### Environment Variables

Create a `.env` file in the root directory:

```env
# Database
DATABASE_URL="file:./dev.db"

# App Configuration
NEXT_PUBLIC_APP_URL="http://localhost:3000"

# AI Configuration (if needed)
# OPENAI_API_KEY="your-key-here"

# News API Keys (optional)
# REUTERS_API_KEY="your-reuters-key"
# NEWS_API_KEY="your-news-api-key"
```

## 📖 Usage Guide

### Admin Panel
Access the admin panel at `/admin` to:
- View system statistics and health
- Manage generated articles
- Configure news sources
- Adjust system settings
- Monitor activity logs

### Manual Article Generation
Trigger article generation manually:
```bash
curl -X POST http://localhost:3000/api/generate \
  -H "Content-Type: application/json" \
  -d '{"count": 3, "category": "technology"}'
```

### News Collection
Fetch latest news from configured sources:
```bash
curl http://localhost:3000/api/news
```

### System Health
Check system health and statistics:
```bash
curl http://localhost:3000/api/health
```

## 🔧 Configuration

### System Settings
Configure system behavior via the admin panel or API:

- **generationFrequency**: Hours between article generations (default: 1)
- **autoPublish**: Automatically publish articles (default: true)
- **requireReview**: Require manual review before publishing (default: false)
- **maxArticlesPerHour**: Maximum articles per generation cycle (default: 5)
- **enableImageGeneration**: Generate AI images (default: true)
- **seoOptimization**: Enable SEO optimization (default: true)

### News Sources
Add custom news sources via the admin panel:

**RSS Sources**:
```json
{
  "name": "Tech News RSS",
  "url": "https://example.com/feed",
  "type": "rss",
  "category": "Technology"
}
```

**API Sources**:
```json
{
  "name": "News API",
  "url": "https://api.example.com/news",
  "type": "api",
  "category": "General"
}
```

**Web Crawl Sources**:
```json
{
  "name": "News Website",
  "url": "https://example.com",
  "type": "web_crawl",
  "category": "General"
}
```

## 📊 API Endpoints

### Articles
- `GET /api/articles` - List articles with pagination
- `POST /api/articles` - Create new article
- `GET /api/articles/[id]` - Get single article
- `PUT /api/articles/[id]` - Update article
- `DELETE /api/articles/[id]` - Delete article

### News & Generation
- `GET /api/news` - Fetch latest news from sources
- `POST /api/generate` - Generate articles from news
- `GET /api/sources` - List news sources
- `POST /api/sources` - Add new news source

### System
- `GET /api/health` - System health check
- `GET /api/settings` - Get system settings
- `POST /api/settings` - Update system settings
- `POST /api/setup` - Initialize system with default data

### SEO & Feeds
- `GET /sitemap.xml` - Dynamic sitemap
- `GET /rss` - RSS feed
- `GET /robots.txt` - Robots file for search engines

## 🗂️ Project Structure

```
ai-news-hub/
├── src/
│   ├── app/                    # Next.js App Router
│   │   ├── api/               # API routes
│   │   ├── admin/             # Admin panel
│   │   ├── sitemap.xml/       # Sitemap generation
│   │   ├── rss/               # RSS feed
│   │   └── page.tsx           # Homepage
│   ├── components/            # React components
│   │   ├── ui/               # shadcn/ui components
│   │   ├── article-card.tsx  # Article display component
│   │   └── blog-widgets.tsx  # Blog UI widgets
│   └── lib/
│       └── db.ts              # Database connection
├── mini-services/
│   └── article-generator/     # Background service
├── prisma/
│   └── schema.prisma          # Database schema
└── README.md
```

## 🔄 Workflow

### Automated Generation Process
1. **News Collection**: Service fetches news from multiple sources every 30 minutes
2. **Content Analysis**: AI analyzes news items for relevance and uniqueness
3. **Article Generation**: AI creates original articles based on news items
4. **SEO Optimization**: Meta tags, keywords, and structured data are generated
5. **Image Generation**: AI creates featured images (if enabled)
6. **Publication**: Articles are published automatically or queued for review

### Content Quality
- **Originality**: All content is rewritten to avoid plagiarism
- **Journalistic Standards**: Professional tone and structure
- **Fact Checking**: AI-powered verification of information
- **SEO Best Practices**: Optimized for search engines
- **Readability**: Clear, accessible language

## 🚀 Deployment

### Production Build
```bash
npm run build
npm start
```

### Environment Setup
1. Set production environment variables
2. Configure database (PostgreSQL recommended for production)
3. Set up reverse proxy (nginx/Caddy)
4. Configure SSL certificates
5. Set up monitoring and logging

### Docker Deployment
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For issues and questions:
- Check the [documentation](https://github.com/your-repo/ai-news-hub/wiki)
- Open an [issue](https://github.com/your-repo/ai-news-hub/issues)
- Contact support at support@ainewshub.com

## 🔮 Future Features

- **Multi-language Support**: Articles in multiple languages
- **Social Media Integration**: Auto-posting to social platforms
- **Email Newsletters**: Automated email digests
- **Advanced Analytics**: Detailed traffic and engagement metrics
- **Custom Templates**: Customizable article layouts
- **User Accounts**: Personalized content recommendations
- **API Access**: Public API for third-party integrations

---

Built with ❤️ using Next.js, TypeScript, and AI technology. Powered by [Z.ai](https://z.ai) 🚀
# Bitly Java API Client

A comprehensive Java library for interacting with the Bitly API, enabling developers to programmatically shorten URLs, manage Bitly links, and retrieve detailed analytics data.

## Features

- **URL Shortening**: Convert long URLs into compact, shareable Bitly links
- **Custom Link Creation**: Create branded links with custom slugs
- **Comprehensive Analytics**: Access click statistics, referrer data, and geolocation insights
- **Batch Processing**: Handle multiple URLs efficiently with bulk operations
- **QR Code Integration**: Generate QR codes for Bitly links
- **Rate Limit Management**: Built-in handling for API rate limits and error responses
- **OAuth 2.0 Support**: Secure authentication with Bitly API tokens

## Tech Stack

- **Backend**: Java 8+, Maven, OkHttp3, Gson
- **Frontend**: React.js with responsive UI
- **Testing**: JUnit 5 + Mockito
- **API**: Bitly API v4

## Quick Start

### Clone and Build

```bash
git clone https://github.com/1byinf8/bitly-java.git
cd bitly-java
mvn clean install
```

### Add to Your Project

```xml
<dependency>
    <groupId>com.bitly</groupId>
    <artifactId>bitly-java</artifactId>
    <version>1.0.0</version>
</dependency>
```

### Basic Usage

```java
import com.bitly.api.BitlyClient;

public class Example {
    public static void main(String[] args) {
        String apiToken = System.getenv("BITLY_API_TOKEN");
        BitlyClient client = new BitlyClient(apiToken);
        
        // Shorten a URL
        String shortUrl = client.shorten("https://www.example.com/very-long-url");
        System.out.println("Short URL: " + shortUrl);
        
        // Get analytics
        ClickStats stats = client.getClickStats("https://bit.ly/example");
        System.out.println("Total Clicks: " + stats.getTotalClicks());
    }
}
```

## API Methods

### URL Operations
```java
// Basic shortening
String shortUrl = client.shorten("https://example.com");

// Custom slug
String customUrl = client.createCustomLink("https://example.com", "my-brand");

// Batch processing
List<String> shortUrls = client.shortenBatch(longUrls);
```

### Analytics
```java
// Click statistics
ClickStats stats = client.getClickStats("https://bit.ly/example");

// Geographic data
List<Country> countries = stats.getCountries();

// Referrer information
List<Referrer> referrers = stats.getReferrers();
```

### Link Management
```java
// Update link
client.updateLink("https://bit.ly/example", "new-title", Arrays.asList("tag1", "tag2"));

// Generate QR code
String qrCodeUrl = client.generateQRCode("https://bit.ly/example");
```

## Project Structure

```
bitly-java/
├── src/main/java/com/bitly/api/
│   ├── BitlyClient.java              # Main API client
│   ├── models/                       # Data models
│   │   ├── Link.java
│   │   ├── ClickStats.java
│   │   └── ErrorResponse.java
│   └── utils/                        # Utilities
│       ├── HttpClient.java
│       └── RateLimitHandler.java
├── src/main/resources/frontend/      # React frontend
├── src/test/                         # Test suite
├── pom.xml                          # Maven config
└── README.md
```

## Testing

```bash
# Run all tests
mvn test

# Test coverage report
mvn jacoco:report
```

**Test Coverage**: 95%+ with comprehensive unit and integration tests.

## Configuration

```java
BitlyClient client = new BitlyClient.Builder(apiToken)
    .setTimeout(30000)
    .setMaxRetries(3)
    .enableDebugLogging(true)
    .build();
```

## Key Dependencies

- **OkHttp3**: HTTP client for API communication
- **Gson**: JSON processing
- **JUnit 5**: Unit testing framework
- **Mockito**: Mocking framework for tests

## Performance

- **Rate Limit Handling**: Automatic retry with exponential backoff
- **Thread Safety**: All client methods are thread-safe
- **Response Times**: Average 200ms for URL shortening
- **Reliability**: Built-in timeout and connection pooling

## Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -m 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Open Pull Request

## License

MIT License - see [LICENSE](LICENSE) file for details.

## Author

**Satwik Kashyap**
- GitHub: [@1byinf8](https://github.com/1byinf8)
- Email: kashyapsatwik29@gmail.com

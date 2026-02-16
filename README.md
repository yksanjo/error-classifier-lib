# Error Classifier Library

Error classification and retryability determination for Node.js applications.

## Features

- **Error Classification**: Categorize errors as timeout, rate_limit, authentication, model, quality, network, system
- **Retryability**: Determine if an error should trigger a retry
- **Fallback**: Identify when to fallback to alternative services
- **Custom Config**: Extend with custom error codes

## Installation

```bash
npm install error-classifier-lib
```

## Usage

```typescript
import { ErrorClassifier, ErrorCode } from 'error-classifier-lib';

const classifier = new ErrorClassifier({
  maxRetries: 3,
  baseDelay: 1000,
  maxDelay: 30000,
  backoffMultiplier: 2,
  jitter: false
});

const result = classifier.classify(ErrorCode.TIMEOUT);
console.log(result.classification); // 'timeout'
console.log(result.retryable); // true
console.log(result.shouldFallback); // true
```

## Error Codes

- Network: TIMEOUT, CONNECTION_ERROR, DNS_ERROR
- Auth: AUTHENTICATION_ERROR, INVALID_API_KEY, PERMISSION_DENIED
- Rate Limit: RATE_LIMIT, QUOTA_EXCEEDED
- Model: MODEL_NOT_FOUND, MODEL_OVERLOADED, CONTEXT_LENGTH_EXCEEDED
- Quality: INVALID_RESPONSE, PARSE_ERROR, EMPTY_RESPONSE
- Quality Gates: QUALITY_THRESHOLD_NOT_MET, LATENCY_TOO_HIGH
- System: INTERNAL_ERROR, SERVICE_UNAVAILABLE, UNKNOWN_ERROR

## License

MIT

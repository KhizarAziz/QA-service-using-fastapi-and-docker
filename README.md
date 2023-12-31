## Introduction
This repo have a starter code for Question and Answering Service developed with FastAPI, Docker-compose and MySQL.

## Components
The repository contains three services:

1. **Question-Answer Service**: Located in the `question_answer_service` directory. Takes a question, calls answer macthing service to get an answer and returns the answer.
  
2. **Answer Matching Service**: Located in the `answer_matching_service` directory. Takes a question and matches (using tf-idf and linear kernel) it to a relevant answer in a knowledge base.
  
3. **Conversation History Service**: Located in the `conversation_history_service` directory. Stores question and answer pairs into a knowledge base (local db for now).

## Prerequisites
- Docker
- Docker Compose

## How to Run
1. Download, Setup and run Docker!

2. Clone this repository.

3. Set path to wherever you want to save your sqlite DB file:
```bash
export DB_URL=YOUR_DB_URL  # Example: sqlite:///commons/knowledge_base.db
```

4. Build and run the services:
```bash
docker-compose up
```

5. (Optional) Re-run failed service: (incase a service stopped right after booting up)
```bash
docker-compose up FAILED_SERVICE_NAME
```

## API Endpoints

### Question Answer Service
- **Port**: 8000
**POST `/ask/`**

- **Description**: Takes in a question and returns an answer from the knowledge base.
- **Request Body**: 
    ```json
    {
        "question": "What is the capital of France?"
    }
    ```
- **Response**: 
    ```json
    {
        "answer": "Paris"
    }
    ```

### Answer Matching Service
- **Port**: 8001
**POST `/match/`**

- **Description**: Takes in a question and finds a relevant question in the knowledge base, returns the matching answer.
- **Request Body**: 
    ```json
    {
        "question": "Tell me the French capital."
    }
    ```
- **Response**: 
    ```json
    {
        "matched_question": "What is the capital of France?",
        "answer": "Paris"
    }
    ```

### Conversation History Service
- **Port**: 8002
**POST `/store/`**

- **Description**: Stores the question and answer pair into the knowledge base.
- **Request Body**: 
    ```json
    {
        "question": "What is the capital of France?",
        "answer": "Paris"
    }
    ```
- **Response**: 
    ```json
    {
        "status": "Stored"
    }
    ```

**GET `/fetch_last/`**

- **Description**: Fetches the last N conversations from the knowledge base.
- **Query Parameters**: `n` (default: 5)


## Future works
- Improve question matching service (Word2Vec, BERT)
- Utilize BloomFilter for faster matching.
- Have a better matching threshold.
- Improve architecture (e.g params as models (question))


## Testing
(TBD) To be done

## Troubleshooting
(TBD) To be done

## Contributions
Feel free to submit pull requests or open issues to contribute to the project.

## License
(TBD)

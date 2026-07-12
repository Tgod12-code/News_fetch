# News_fetch
This is about fetching different kind of news over the internet using newsapi.
## How to Run
1. Clone the repo
2. Install dependencies: `pip install fastapi uvicorn requests`
3. Run server: `uvicorn NEWS:app --reload`
4. Test API: `http://127.0.0.1:8000/news?query=technology&country=in`


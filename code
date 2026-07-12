from fastapi import FastAPI, HTTPException, Query
import requests

app = FastAPI()

NEWS_API_KEY = "ae23c83443e26947cb26ec2d8f657e4b"
BASE_URL = "https://gnews.io/api/v4/search"

@app.get("/")
def read_root():
    return {"message": "News API Ready! Use /news?query=technology"}

@app.get("/news")
def get_news(
    query: str = Query(..., description="Search keyword like sports, technology, cricket"),
    country: str = Query(..., description="Country code: us, in, gb, etc."),
    page: int = Query(1, description="Page number"),
    max_results: int = Query(5, description="Articles per page (max 10)")
):
    try:
        params = {
            "token": "ae23c83443e26947cb26ec2d8f657e4b",
            "q": query,
            "country": country,
            "language": "en",
            "page": page,
            "max": max_results
        }
        response = requests.get(BASE_URL, params=params)
        data = response.json()
        

        if data.get("status") == "error":
            raise HTTPException(status_code=400, detail=data.get("message"))

        news_list = []
        for article in data.get("articles", []):
            news_list.append({
                "title": article["title"],
                "author": article.get("author", "Unknown"),
                "description": article.get("description", "No description"),
                "url": article["url"],
                "image": article.get("image", "No image")
            })
            

        return {"query": query, "page": page, "count": len(news_list), "news": news_list}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))





# Run command: uvicorn news_api:app --reload   

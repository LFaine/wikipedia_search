# for fetching wikipedia articles
import wikipedia
# for fetching sections of the chosen article
import sections

# Function to search the query 
# that is either entered
# by user 
def search(query):
    try:
        result=wikipedia.summary(query)
        result=result.replace('. ','.\n') #This replace function is used to prevent the summary from
        result=result.replace(', ',',\n') #running offscreen by linebreaking after each period or comma
    except wikipedia.WikipediaException:
        print('Try another search, that page does not exist or your search is not specific enough.')
    finally:
        if query=='random':
            result=wikipedia.random(5)
            print(result)
        else:
            return (result)

def print_sections(query):
    if query=='random':
        print(wikipedia.random(5))
    else:
        page = wikipedia.page(query)
        sections=page.sections #from wikipedia-sections api
        print('The sections of this article are:','\n',sections)
        ans=input('Choose a section to read: ')
        for ans in sections:
            print(page.section(ans))
        print('Run again for a new article!')

query=input('Type your search here, or "random" to get suggestions: ')
print(search(query))
print_sections(query)

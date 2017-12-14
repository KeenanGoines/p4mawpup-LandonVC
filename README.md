# p4mawpup-LandonVC
p4mawpup-LandonVC created by GitHub Classroom
this is a readme

from bs4 import BeautifulSoup
import requests
from twilio.rest import Client

url = 'https://postmates.com/los-angeles'
account_sid = 'XXX'
auth_token = 'XXX'
twilio_phone_number = '+15558675309'
my_phone_number = '+15551234567'

webpage = requests.get(url)
soup = BeautifulSoup(webpage.text, 'html.parser')

free_food = [s for s in soup.body.stripped_strings if 'free' in s.lower()]

if free_food:
    body = 'Free Postmates!\n\n' + '\n'.join(free_food)
    client = Client(account_sid, auth_token)
    client.messages.create(
        body=body,
        to=my_phone_number,
        from_=twilio_phone_number
    )

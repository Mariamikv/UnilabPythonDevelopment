# Flask საწყისები
[ოფიციალური გვერდი](https://palletsprojects.com/p/flask/) | [დოკუმენტაცია](https://flask.palletsprojects.com/en/1.1.x/) | [GitHub](https://github.com/pallets/flask)

ფლასკი Python-ში დაწერილი ვებ მიკრო ფრიმვორკია. Flask-ის გამოყენებით მარტივად და სწრაფად შეგიძლიათ ააწყოთ მარტივი ვებ სერვისები
პითონში და პროექტის გართულებასთან ერთად დახუნძლოთ აპლიკაცია უამრავი შესაძლებლობით, რომელსაც [flask-ის ნაკრებები და third-party
ბიბლიოთეკები გვთავაზობენ](https://www.fullstackpython.com/flask-extensions-plug-ins-related-libraries.html).

## სარჩევი
- [დაყენება](დაყენება)
- [დამატებითი რესურსები](#დამატებითი-რესურსები)


## დაყენება
### დაყენება pip მენეჯერით

```python
pip install flask
```

### დაყენება conda მენეჯერით

```python
conda install flask
```


ინსტალაციის წარმატებით დასრულების შესამოწმებლად, ინტერპრეტატორის გამოყენებით სცადეთ ბიბლიოთეკის შემოტანა:


```python
from flask import Flask
```

თუ b

პაკეტიდან სახელწოდებით flask შემოგვაქვს კლასი Flask.
სტანდარტულად პაკეტის სახელი იწყება პატარა ასოთი, ხოლო კლასის დიდით.

#### საბაზისო Flask აპლიკაცია


```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "გამარჯობა"

app.run(port = 5000)
```

     * Serving Flask app "__main__" (lazy loading)
     * Environment: production
       WARNING: This is a development server. Do not use it in a production deployment.
       Use a production WSGI server instead.
     * Debug mode: off
    

     * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
    127.0.0.1 - - [30/Mar/2020 01:31:33] "[37mGET / HTTP/1.1[0m" 200 -
    127.0.0.1 - - [30/Mar/2020 01:31:37] "[37mGET / HTTP/1.1[0m" 200 -
    

ინტერნეტ ბრაუზერით ლოკალურ სერვერთან დაკავშირებისას (ჩემს შემთხვევაში მისამართზე: http://127.0.0.1:5000/), საინფორმაციო ველში გამოვა ჩანაწერი "გამარჯობა"

### REST-ის გამოყენების პრინციპები
#### HTTP Verbs - მოთხოვნის მეთოდები

სერვერული პროგრამის ფუნცქიია მიიღოს ვებ მოთხოვნები.

ვებ საიტზე შესვლისას, სერვერზე გაშვებული პროგრამის ტერმინალის ფანჯარაში გამოჩნდება ინფორმაცია (ლოგი) შემოსული მოთხოვნის შესახებ, მაგ.:

127.0.0.1 - - [30/Mar/2020 01:31:33] "GET / HTTP/1.1" 200 -

მოცემული ლოგის სტრუქტურა შემდეგნაირია:

მისამართი - - [თარიღი(დღე/თვე/წელი საათი:წუთი:წამი)] "ტიპი  მისამართი  პროტოკოლი" სტატუსი -

**მოთხოვნის მეთოდების ტიპები:**

**GET** - მონაცემის ამოღება
**POST** - მონაცემის მიღება და გამოყენება
**PUT** - მონაცემის შექმნა ან განახლება
**DELETE** - მონაცემის ამოშლა

სერვერის მხარეს ყველა მოთხოვნის ტიპი ერთნაირად მუშავდება. განსხვავებული ტიპები მეთოდების კატეგორიზაციასა და გარჩევაში გვეხმარება. ერთ მისამართზე შესაძლებელია რამოდენიმე სხვადასხვა ტიპის მოთხოვნის გამოყენება, მაგალითად:

**"GET /item/student"** - რესურსის ამოღება

**"POST /item/student + პატარმეტრი"** - რესურსისთვის პარამეტრების მიწოდება

**"PUT /item/student + პარამეტრი"** - პარამეტრის მიხედვით რესურსის შექმნა ან განახლება

**"DELETE /item/student"** - რესურსის ამოშლა

კონკრეტულ მაგალითში, /course/student მისამართზე შეგვიძლია მანიპულირება ინდივიდუალურ რესურზე(item resource). თუმცა მოთხოვნის გაგზავნა ანალოგურად არის შესაძლებელია რესურსების სიაზეც (itemList resource) მისამართზე /item.

REST ტიპის მოთხოვნა არის **Stateless** მოთხოვნა, რაც გულისხმობს რომ ერთი მოთხოვნა ვერ იქნება დამოკიდებული მეორე მოთხოვნაზე, რადგან მათ შორის არ არის პირდაპირი პროგრამული კავშირი. შესაბამისად, მოთხოვნის დამუშავებისას, პროგრამა ფუნქციონირებს კონკრეტული მოთხოვნის პარამეტრების მიხედვით. 


### App Endpoints - რესურსის მისამართები

რესურსის ტიპები სერვერისა და ბრაუზერისთვის ურთიერთშებრუნებულ დანიშნულებას ასრულებს:

**ტიპი - ფუნცქიონალი სერვერისთვის - ფუნქციონალი ბრაუზერისთვის**

POST - მონაცემის მიღება - მონაცემის მიწოდება
GET - მხოლოდ მონაცემის დაბრუნება - მონაცემის მიღება

Flask-ით რესურსის წვდომის შესაქმნელად ვიყენებთ როუთებს. როუთის გასამართად გვჭირდება მივუთითოთ რესურსის მისამართი,  მაგალითად საკლასო ოთახზე წვდომის გასამართად ვწერთ:


```python
@app.route('/classroom', methods = ['POST'])
```

ერთი როუთზე წვდომის დაშვება შესაძლებელია სხვადასხვა ტიპის მეთოდებით. ამისთვის methods-ს უნდა მივანიჭოთ შესაბამისი პარამეტრი, მაგალითად: methods = ['POST', 'GET']

როუთის შემდეგ საჭიროა მეთოდის გაწერა. მაგალითად:


```python
@app.route('/classroom', methods = ['POST'])
def create_classroom():
    
    # კოდი ბაზაში საკლასო ოთახის დასამატებლად
    
    return 200, 'ok'
```

200 ok არის სტატუს კოდი რომელიც მოთხოვნის მხარეს ატყობინებს რომ მოთხოვნა წარმატებით შესრულდა. (ფლასკში ინტეგრირებულ სტატუს კოდებზე დოკუმენტაცია: https://www.flaskapi.org/api-guide/status-codes/)

flask-ის გამოყენებით, წინასწარ გაწერის გარეშე, შესაძლებელია მივწვდეთ რესურსის სიაში არსებულ ან პროგრამულად ჩამატებულ ნებისმიერ ელემენტს <string:name> სინტაქსით, რომლის მნიშვნელობაც მეთოდს გადაეცემა პარამეტრად. მაგალითად:


```python
@app.route('/classroom/<string:name>', methods = ['GET'])
def info_classroom(name):
    
    # კოდი ბაზიდან საკლასო ოთახზე ინფორმაციის ამოსაღებად
    
    return classroomInfo
```

ამ როუთს შევძლებთ მივაკითხოვთ მისამართზე: <localhost:5000/classroom/pythonclass>

მეთოდს კი პარამეტრად გადაეცემა მნიშვნელობა "pythonclass", რის გამოყენებასაც შევძლებთ კოდის ფუნქციონალურ ნაწილში. აუცილებელია რომ როუთში გაწერილ მისამართში ცვლადის და მეთოდში გაწერილი ცვლადის სახელი იყოს იდენტური.

მიუხედავად იმისა რომ მეთოდის დასახელებას პროგრამის მუშაობისთვის მნიშვნელობა არ აქვს, მას უნდა ერქვას უნიკალური სახელი.

ფინალური კოდი:


```python
from flask import Flask, request

app = Flask(__name__)

cinemas = [
    {"name": "Rustaveli",
     "address": "Kostava st. 36"}
]

@app.route('/<string:name>', methods=['GET']) #/
def get(name):
    for cinema in cinemas:
        if name == cinema['name']:
            return {"address": cinema['address']}
    return {"message": "მონაცემი ვერ მოიძებნა"}, 400

@app.route('/<string:name>', methods=['POST']) #/
def post(name):
    request_data = request.get_json()
    for cinema in cinemas:
        if name == cinema['name']:
            return {"message": "მონაცემი უკვე არსებობს"},400
    new_cinema = {
        "name": name,
        "address": request_data['Address']
    }
    cinemas.append(new_cinema)
    return {"message": cinemas}

@app.route('/<string:name>', methods=['PUT']) #/
def put(name):
    print("new request")
    request_data = request.get_json(force=True)
    print(request_data)
    new_cinema = next(filter(lambda x: x['name'] == name, cinemas), None)
    if new_cinema:
        new_cinema.update(request_data)
    else:
        cinema = {'name': name,
                  'address': request_data['address']}
        cinemas.append(cinema)
    return {"message": cinemas}

@app.route('/<string:name>', methods=['DELETE']) #/
def delete(name):
    global cinemas
    cinemas = list(filter(lambda x: x['name'] != name, cinemas))
    return {"message": cinemas}

app.run(port = 5000)
```

## დამატებითი რესურსები
- [უამრავი Flask-ს მორგებული ბიბლიოთეკა, პლაგინები და რესურსები](https://github.com/humiaozuzu/awesome-flask)
- 

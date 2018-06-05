## 1. Project Title: **PIE**

## 2. Overview
#### 2.1 Big Picture of **PIE** system
![Big Picture](https://github.com/nguyenthihoangphuong/images/blob/Backend/PIE%20system.png?raw=true)

#### 2.2 Description:
**- Backend:** 
> The back end application which is written as micro-services for Pie Fleet that contains 4 main services: fenice, parrot, eagle, hermes

**- Frontend:**
> The front end web application for Pie Fleet. It connect to BackEnd to get/push data through APIs.

## 3. Detail System Guideline
### 3.1 Backend:
#### 3.1.1 Components in the system

**- Fenice:**
> Execute the Pie's business logic, connect database (mysql).

**- Parrot:** 
> Http gateway

**- Eagle:** 
> Connect cassandra, manage all object point: vehicle, route, leg, etc.

**- Hermes:** 
> Send messages(torilio) & email(sendgrid).

**How to save object points?**
> **Live Map:** 
> > Show position of driver job in real time. Mobile will push position to *parrot*, *fenice*. *Eagle* server will save this value on cassandra.
> > 
> > ![Object points](https://github.com/nguyenthihoangphuong/images/blob/Backend/ObjectPoint.png?raw=true)

#### 3.1.2 Installing:
> [Backend_installing](https://github.com/piemapping/backend/tree/feature/DEVOPS-244)

#### 3.1.3 Documents:

**- Testing**

> [Manual Test](https://docs.google.com/spreadsheets/d/1ToHisXyfIsDtZlo8jC60lPzzWNz8Vs0szuJJczNzkoY/edit#gid=1441377163)

> [Functional Test](https://github.com/piemapping/frontend/tree/develop/functional-test/features)

**- User guidle**


### 3.2 Frontend:
#### 3.2.1 Installing:
> [Frontend_installing](https://github.com/piemapping/frontend)

## 4. Contact
Team: PIE-Backend

| Name          | Position      | Email                |
| ------------- |:-------------:| --------------------:|
| Ân            | PM            | an@dwarvesv.com      |
| Huy           | Developer     | huy@dwarvesv.com     |
| Quang         | Devops        | quang@dwarvesv.com   |

## 5. Version
| Version          | Release date      | Description          |
| ---------------- |:-----------------:| --------------------:|
| V1.0.1           | Sep 10th, 2016    |                      |

## 6. License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

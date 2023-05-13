openapi: 3.0.2
info:
  version: 1.0.0
  title: flyswing
  description: "This is the Open API documentation for the REST API of our beloved application **Wall of Tweets** deployed at <https://fib-asw-wotapi.fly.dev/>. <br>All operations are executable. Only one operation requires authentication: `deleteTweet`. In this case, you must **Authorize** your request by providing the token value you got when you created the tweet."
servers:
  - url: 'https://flyswing-api.onrender.com'
paths:
  /users:
    
    get:
      tags:
      - users
      summary: Retrieves all the Issues
      operationId: getAllIssues
      responses:
        200:
          description: successful operation
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
  

                
  
  /users/new/:
    post:
      tags:
      - users
      summary: Create a users
      operationId: createUsers
      requestBody:
        description: Provide the username  of the new User
        content:
          application/json:
            schema:
              required:
              - username
              type: object
              properties:
                username:
                  type: string
                  minLength: 4
                  example: 'My name'
        required: true
      responses:
        200:
          description: Created Tweet
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        404:
          description: 'Error: Not Found'
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResult'
              examples:
                errorExample:
                  $ref: '#/components/examples/error404'
                  
                  
  
  /users/{username}/:
    put:
      tags:
      - users
      summary: Update points of a users
      operationId: updateUsers
      parameters:
        - name: username
          in: path
          description: username of person to update
          required: true
          schema:
            type: integer
            format: int64
      requestBody:
        description: Provide the points of the User
        content:
          application/json:
            schema:
              required:
              - points
              type: object
              properties:
                points:
                  type: integer
                  minLength: 4
                  example: '0'
        required: true
        
      responses:
        200:
          description: Created Tweet
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        404:
          description: 'Error: Not Found'
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorResult'
              examples:
                errorExample:
                  $ref: '#/components/examples/error404'



components:
  schemas:
    User:
      type: object
      properties:
        username:
          type: integer
          format: int64
          example: 'tania'
        points:
          type: integer
          format: int64
          example: '0'
    ErrorResult:
      type: object
      properties:
        message: 
          type: string
          example: 'Content is too long (maximum is 280 characters)'
      required:
        - message
  examples:
    error400:
      value:
        message: "Content is too long (maximum is 280 characters)"
    error401:
      value:
        message: "You provided no token"
    error403:
      value:
        message: "You provided an invalid token"
    error404:
      value:
        message: "There is no tweet with 'id'=8"
  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      name: Authorization
      in: header
      
      
      

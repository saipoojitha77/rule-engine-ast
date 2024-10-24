# rule-engine-ast
# Project Title 
          Rule Engine with Abstract Syntax Tree (AST)
## Description
          This project implements a rule engine to evaluate user eligibility based on customizable conditions using an Abstract Syntax Tree (AST). Users can define rules involving attributes such as age, department,
          income, and experience. The system supports dynamic rule creation, combination, modification, and evaluation.
### Features
          •	Dynamic Rule Creation: Define conditional rules as ASTs for flexible manipulation.
          •	Rule Combination: Combine multiple rules efficiently to create complex eligibility conditions.
          •	Rule Evaluation: Evaluate user data (e.g., age, salary, department) against the rules to determine eligibility.
          •	Error Handling: Validate rules and input data, ensuring integrity.
          •	Rule Modification: Modify existing rules dynamically (e.g., change operators or operand values).
          •	Sample Rules: Test with predefined rules (e.g., age and salary constraints).
#### Data Structure
          The Abstract Syntax Tree (AST) is composed of nodes where:
            •	Each operator node (e.g., AND, OR) has left and right child nodes.
            •	Each operand node represents a condition (e.g., age > 30).
          Sample AST node structure:
            python
              class ASTNode:
                def __init__(self, node_type, left=None, right=None, value=None):
                     self.node_type = node_type  # "operator" or "operand"
                     self.left = left
                     self.right = right
                     self.value = value
##### Data Stroage
         Rules and metadata are stored in a database. 
           •	MongoDB: Ideal for nested and flexible structures.
           •	PostgreSQL: Suitable for storing rules in a relational format.
         Sample MongoDB schema:
            json
               {
                 "rule_id": "rule1",
                 "rule_ast": {
                 "node_type": "operator",
                  "left": {
                    "node_type": "operand",
                   "value": "age > 30"
                    },
                 "right": {
                   "node_type": "operand",
                   "value": "department = 'Sales'"
                    }
                    },
                  "created_at": "2024-10-24T12:34:00Z"
                  }
###### Example Rules
         1.	Rule 1:
          ((age > 30 AND department = 'Sales') OR (age < 25 AND department = 'Marketing')) AND (salary > 50000 OR experience > 5)
         2.	Rule 2:
         (age > 30 AND department = 'Marketing') AND (salary > 20000 OR experience > 5)
###### Installation
          Prerequisites:
           •	Python 3.12.0
           •	MongoDB or PostgreSQL
           Setup:
           1.	Clone the repository:
              git clone https://github.com/saipoojitha77/rule-engine-ast.git
              cd rule-engine-ast
           2.	Install dependencies:
              pip install -r requirements.txt
           3.	Configure database connection in the environment variables.
           4.	Start the application:
               uvicorn app:app --reload
###### API Design
        1.	Create Rule: Converts a rule string into an AST representation.
             o	Endpoint: /create_rule
             o	Method: POST
             o	Input:
                        json
                         { "rule_string": "age > 30 AND department = 'Sales'" }
             o	Response:
                       json
                        { "status": "success", "ast": { ... } }
        2.	Combine Rules: Combines multiple rules into one AST.
             o	Endpoint: /combine_rules
             o	Method: POST
             o	Input:
                    json
                     { "rules": ["rule1", "rule2"] }
             o	Response:
                    json
                     { "status": "success", "combined_ast": { ... } }
        3.	Evaluate Rule: Evaluates a rule against user data.
             o	Endpoint: /evaluate_rule
             o	Method: POST
             o	Input:
                     json
                       {
                          "rule_id": "combined_rule",
                             "data": {
                                 "age": 35,
                                 "department": "Sales",
                                 "salary": 60000,
                                 "experience": 3
                                 }
                          }
              o	Response:
                        json
                          { "status": "success", "eligible": true }
###### Test Cases
            1.	Create Rule: Ensure ASTs are correctly generated from strings.
            2.	Combine Rules: Test the combination of rules.
            3.	Evaluate Rule: Test with different sets of user data and rule conditions.
            4.	Error Handling: Test invalid inputs, missing operators, and unknown attributes.
###### Future Enhancement
            •	Rule Modification: Add features to update existing ASTs dynamically.
            •	User-Defined Functions: Support for advanced conditions with custom logic.
            •	UI: Develop a user-friendly interface for managing rules.
###### Contributions
            Contributions are welcome! Please create a pull request with your changes or open an issue for any suggestions or bugs.
###### License
            This project is licensed under the MIT License.
            

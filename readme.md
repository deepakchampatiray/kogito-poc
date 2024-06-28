# kogito-poc

## Task List GraphQL Query
{
	"operationName": "getTasksForUser",
	"query": "query getTasksForUser($whereArgument: UserTaskInstanceArgument, $offset: Int, $limit: Int, $orderBy: UserTaskInstanceOrderBy) {\n  UserTaskInstances(where: $whereArgument, pagination: {offset: $offset, limit: $limit}, orderBy: $orderBy) {\n    id\n    name\n    referenceName\n    description\n    priority\n    processInstanceId\n    processId\n    rootProcessInstanceId\n    rootProcessId\n    state\n    actualOwner\n    adminGroups\n    adminUsers\n    completed\n    started\n    excludedUsers\n    potentialGroups\n    potentialUsers\n    inputs\n    outputs\n    lastUpdate\n    endpoint\n    __typename\n  }\n}\n",
	"variables": {
		"limit": 10,
		"offset": 0,
		"orderBy": {
			"lastUpdate": "DESC"
		},
		"whereArgument": {
			"and": [
				{
					"or": [
						{
							"actualOwner": {
								"equal": "alice"
							}
						},
						{
							"and": [
								{
									"actualOwner": {
										"isNull": true
									}
								},
								{
									"not": {
										"excludedUsers": {
											"contains": "alice"
										}
									}
								},
								{
									"or": [
										{
											"potentialUsers": {
												"contains": "alice"
											}
										},
										{
											"potentialGroups": {
												"containsAny": [
													"HR",
													"user"
												]
											}
										}
									]
								}
							]
						}
					]
				},
				{
					"and": [
						{
							"state": {
								"in": [
									"Ready",
									"Reserved"
								]
							}
						}
					]
				}
			]
		}
	}
}
## End of Task List

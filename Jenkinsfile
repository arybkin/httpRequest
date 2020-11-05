#!/usr/bin/env groovy
import groovy.transform.Field

@Field
String nodeName = 'master'

@Field
String acBaseFilter = "cat!~Ignore&&cat!~Quarantine&&cat!~Unstable&&cat!~Stabilizing&&cat!~Performance&&cat!~Telerik&&cat!~Memory"
// Filter for Acceptance Test Assemblies
@Field
String nuBaseFilter = "cat!~Ignore&&cat!~Quarantine&&cat!~Performance"
@Field
Map ACTestValidation = [
		"ac": [
				"settings": [
						"path": "AcceptanceTests",
						"pattern": "*AcceptanceTests*.dll",
						"timeout": 40,
						"description": "Multinode Acceptance Tests"
				],
				"categories": [
						"UiComponentTest": [
								"size": 8,
								"filter": "cat==UiComponentTest&&${acBaseFilter}",
								"nodeLabel": nodeName,
						],
						"UILessTest": [
								"size": 40,
								"filter": "cat==UILessTest&&${acBaseFilter}",
								"nodeLabel": nodeName,
						],
						"TestStack.White": [
								"size": 5,
								"filter": "cat==TestStack.White&&${acBaseFilter}",
								"nodeLabel": nodeName,
						],
						"ComponentTest": [
								"size": 1,
								"filter": "cat==ComponentTest&&${acBaseFilter}",
								"nodeLabel": nodeName,
						],
				]
		]
]

@Field
Map BaseTestValidationMultiNode = [
		"nu": [
				"settings": [
						"path": "NUnit",
						"pattern": "*.Test.NUnit*.dll",
						"timeout": 10,
						"description": "Multinode Unit Tests"
				],
				"categories": [
						"OnlyUnitTest": [
								"size": 1,
								"filter": "cat=~UnitTest&&cat!~Local&&${nuBaseFilter}",
								"nodeLabel": nodeName,
						],
				]
		]
]
@Field
Map BaseTestValidationSingleNode = [
		"ac": [
				"settings": [
						"path": "AcceptanceTests",
						"pattern": "*AcceptanceTests*.dll",
						"timeout": 20,
						"nodeLabel": nodeName, // not used, defined in script below
						"description": "Singlenode Acceptance Tests"
				],
				"categories": [
						"ArchitecturalTest": [
								"size": 1,
								"filter": "cat==ArchitecturalTest&&${acBaseFilter}"
						],
						"BestPracticesTest": [
								"size": 1,
								"filter": "cat==BestPracticesTest&&${acBaseFilter}"
						],
						"UndefinedUITest": [
								"size": 1,
								"filter": "cat==UndefinedUITest&&${acBaseFilter}"
						],
				]
		],
		"nu": [
				"settings": [
						"path": "NUnit",
						"pattern": "*.Test.NUnit*.dll",
						"timeout": 10,
						"nodeLabel": nodeName, // not used, defined in script below
						"description": "Singlenode Unit Tests"
				],
				"categories": [
						"UnitComponentTests": [
								"size": 1,
								"filter": "cat!~UnitTest&&cat!~Local&&${nuBaseFilter}"
						]
				]
		]
]
@Field
def Map MinimalTestValidation = [
		"nu": [
				"settings": [
						"path": "NUnit",
						"pattern": "*.Test.NUnit*.dll",
						"timeout": 10,
						"description": "Localnode Unit Tests"
				],
				"categories": [
						"LocalUnitTests": [
								"size": 1,
								"filter": "cat=~Local&&${nuBaseFilter}"
						],
				]
		]
]




configuringworkflow()
NotifyBitbucket()
try{
	println currentBuild.displayName
	println currentBuild.description
	println currentBuild.number
	def parallelizedWork = [:]
	parallelizedWork << validateCode()
	parallelizedWork << validateDoxygen()
	def maxParallelWork = (int) ((parallelizedWork.size() / 2) + 1)
	parallelLimited(parallelizedWork, maxParallelWork)
	///
	Merge()
}
catch(e){
	whatIsMyBuildState()
	currentBuild.result = 'FAILURE'
	throw e
}
finally {
	//	sendEmail()
}

def validateCode(){
	Map codeTestMap=[:]
	node(nodeName){
		CheckoutSCM()
		LoadingScripts()
		UpdatingChangeData()
		Build()
		NDependAnalysis()
		PrepareTestPlans()
		StashTestData()
		LocalTests()
		GenerateTestStages(codeTestMap)
	}
}

def configuringworkflow(){
	stage('configuring workflow') {
		println("log")
	}
}

def Merge(){
	stage('Merge') {
		println("log")
	}
}

def CheckoutSCM(){
	stage('Checkout SCM') {
		println("log")
	}
}

def LoadingScripts(){
	stage('Loading scripts') {
		println("log")
	}
}

def UpdatingChangeData(){
	stage('Updating Change Data') {
		println("log")
	}
}

def Build(){
	stage('Build') {
		println("log")
	}
}

def NDependAnalysis(){
	stage('NDepend Analysis') {
		println("log")
	}

}

def PrepareTestPlans(){
	stage("Prepare Test Plans") {
		def parallelTestFileExtraction = [:]
		parallelTestFileExtraction << generateTestPlans(ACTestValidation)
		parallelTestFileExtraction << generateTestPlans(BaseTestValidationMultiNode)
		parallelTestFileExtraction << generateTestPlans(BaseTestValidationSingleNode)
		parallelTestFileExtraction << generateTestPlans(MinimalTestValidation)

		// run the extracdeletePathPSt test lists steps in parallel
		parallel parallelTestFileExtraction
		println("log")
	}
}

def generateTestPlans(Map TestCategories){
	testPlans=[:]
	TestCategories.each { group ->
		group.value["categories"].each { category ->
			testPlans["${category.key}"] = {
				println("Some plan")
			}
		}
	}
	return testPlans
}

def StashTestData(){
	stage('Stash Test Data') {
		parallel (
				'stashbuild':{println("stashbuild")},
				'stashtestdata':{println("stashtestdata")},
				'stashACtest':{println("stashACtest")},
				'stashUnittest':{println("stashUnittest")},
				'stashTestOutputStructure':{println("stashTestOutputStructure")},
				'stashinfrastructure':{println("stashinfrastructure")},
				'stashbin':{println("stashbin")},
				'stashRPAc':{println("stashRPAc")},
				'stashRPNunit':{println("stashRPNunit")}
		)
	}
}

def GenerateTestStages(codeTestMap){
	stage('Generate Test Stages') {
		println "Generate somth"
		codeTestMap << generateSingleNodeTest(BaseTestValidationSingleNode)
		codeTestMap << generateMultiNodeTest(BaseTestValidationMultiNode)
		codeTestMap << generateMultiNodeTest(ACTestValidation)
		return  codeTestMap
	}
}
def generateSingleNodeTest(Map testPlan){
	singleNodeTestMap = [:]
	def name = testPlan[testPlan.find().key]["categories"].find().key
	singleNodeTestMap[name] = {
		stage(name){
			println name
		}
	}
	return singleNodeTestMap
}

def generateMultiNodeTest(Map testPlan){
	multiNodeTestMap=[:]
	testPlan.each { group ->
		group.value["categories"].each { category ->
			println category
			for (int i = 0; i < category.value["size"]; i++) {
				// variable i prints always value Threads, whereas index increases from 0 to x Threads
				int index = i
				multiNodeTestMap["${group.key}: ${category.key} node-${index}"] = {
					stage("${category.key} node-${index}") {
						println("Run multy node")
					}
				}
			}
		}
	}

	return multiNodeTestMap
}


def LocalTests(){
	stage("local-tests") {
		println("log")
	}
}

def validateDoxygen(){
	def doxygenMap=[:]
	doxygenMap["Build Documentation"] = {
		node(nodeName) {
			CheckoutSCM()
			LoadingScripts()
			BuildDocumentation()
			AnalyzeDocumentation()
		}
	}
	return doxygenMap
}

def BuildDocumentation(){
	stage('Build Documentation') {
		println("log")
	}
}

def AnalyzeDocumentation(){
	stage('Analyze Documentation') {
		println("log")
	}
}

def NotifyBitbucket(){
	stage('Notify Bitbucket') {
		println("log")
	}
}

def parallelLimited(Map<String, Closure> map, int maxConcurrent) {
	def shuffledMap = shuffleMap(map)

	latch = new java.util.concurrent.LinkedBlockingDeque(maxConcurrent)

	// put a number of items into the queue to allow that number of branches to run
	for (int i = 0; i < maxConcurrent; i++) {
		latch.offer("$i")
	}

	def work = [:]

	shuffledMap.each { b ->
		work[b.key] = {
			def thing = null

			while(thing == null) {
				thing = latch.pollFirst();
				if(thing == null) {
					sleep time: 2, unit: 'SECONDS'
				}
			}

			try {
				b.value.call()
			} finally {
				latch.offer(thing)
			}
		}
	}

	parallel work
}

def shuffleMap(Map map) {
	def shuffledMap = [:]

	def keys = new ArrayList(map.keySet());
	Collections.shuffle(keys);
	for (Object o : keys) {
		shuffledMap[o] = map[o]
	}
	return shuffledMap
}

def whatIsMyBuildState() {
	println("~~~ Current Build : Current Result = ${currentBuild.currentResult} || Result = ${currentBuild.result} ~~~")
}

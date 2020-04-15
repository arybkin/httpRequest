#!/usr/bin/env groovy

node("master"){
	configuringworkflow()
	NotifyBitbucket()
	CheckoutSCM()
	LoadingScripts()
	UpdatingChangeData()
	Build()
	NDependAnalysis()

	PrepareTestPlans() // 10 parallel
	StashTestData() // 9 parallel

	LocalTests()
	GenerateTestStages()

	///
	Documentation()
	OnlyUnitTests()
	//54
	ParallelTests()
	///
	Merge()
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
		def parallelizedWork = [:]
		parallelizedWork << ptp(1)
		parallelizedWork << ptp(2)
		parallelizedWork << ptp(3)
		parallelizedWork << ptp(4)
		parallelizedWork << ptp(5)
		parallelizedWork << ptp(6)
		parallelizedWork << ptp(7)
		parallelizedWork << ptp(8)
		parallelizedWork << ptp(9)
		parallelizedWork << ptp(10)
		parallel parallelizedWork
		println("log")
	}
}

def ptp(row){
	def testPlans = [:]
	print row
	testPlan[row] = {row}
	testPlan[row*20] = {row*20}
	return testPlan
}

def StashTestData(){
	stage('Stash Test Data') {
		parallel (
				'1':{println("log")},
				'2':{println("log")},
				'3':{println("log")},
				'4':{println("log")},
				'5':{println("log")},
				'6':{println("log")},
				'7':{println("log")},
				'8':{println("log")},
				'9':{println("log")}
		)
	}
}

def GenerateTestStages(){
	stage('Generate Test Stages') {
		println("log")
	}
}

def LocalTests(){
	stage("local-tests") {
		println("log")
	}
}

def OnlyUnitTests(){
	stage("OnlyUnitTests") {
		println("log")
	}
}

def ParallelTests(){
	stage("ParallelTests") {
		println("log")
	}
}

def Documentation(){
	stage("Build Documentation"){
		CheckoutSCM()
		LoadingScripts()
		BuildDocumentation()
		AnalyzeDocumentation()
	}
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

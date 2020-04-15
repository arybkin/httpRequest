#!/usr/bin/env groovy

node("master"){
	configuringworkflow()
	NotifyBitbucket()
	CheckoutSCM()
	LoadingScripts()
	UpdatingChangeData()
	Build()
	NDependAnalysis()

	StashTestData() // 9 parallel

	def parallelizedWork = [:]
	parallelizedWork << PrepareTestPlans(1)
	parallelizedWork << PrepareTestPlans(2)
	parallelizedWork << PrepareTestPlans(3)
	parallelizedWork << PrepareTestPlans(4)
	parallelizedWork << PrepareTestPlans(5)
	parallelizedWork << PrepareTestPlans(6)
	parallelizedWork << PrepareTestPlans(7)
	parallelizedWork << PrepareTestPlans(8)
	parallelizedWork << PrepareTestPlans(9)
	parallelizedWork << PrepareTestPlans(10)
	parallel parallelizedWork
	parallelLimited(parallelizedWork, 10)

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

def PrepareTestPlans(row){
	stage("Prepare Test Plans $row") {
		println("log")
	}
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

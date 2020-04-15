#!/usr/bin/env groovy

node("master"){
	configuringworkflow()
	NotifyBitbucket()
	CheckoutSCM()
	LoadingScripts()
	UpdatingChangeData()
	Build()
	NDependAnalysis()
	PrepareTestPlans() //10 parallel
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
	stage('Prepare Test Plans') {
		println("log")
	}
}

def StashTestData(){
	stage('Stash Test Data') {
		println("log")
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

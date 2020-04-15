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

	}
}

def Merge(){
	stage('Merge') {

	}
}

def CheckoutSCM(){
	stage('Checkout SCM') {

	}
}

def LoadingScripts(){
	stage('Loading scripts') {

	}
}

def UpdatingChangeData(){
	stage('Updating Change Data') {

	}
}

def Build(){
	stage('Build') {

	}
}

def NDependAnalysis(){
	stage('NDepend Analysis') {

	}

}

def PrepareTestPlans(){
	stage('Prepare Test Plans') {

	}
}

def StashTestData(){
	stage('Stash Test Data') {

	}
}

def GenerateTestStages(){
	stage('Generate Test Stages') {

	}
}

def LocalTests(){
	stage("local-tests") {

	}
}

def OnlyUnitTests(){
	stage("OnlyUnitTests") {

	}
}

def ParallelTests(){
	stage("${category.key} node-${index}") {

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

	}
}

def AnalyzeDocumentation(){
	stage('Analyze Documentation') {

	}
}

def NotifyBitbucket(){
	stage('Notify Bitbucket') {

	}
}

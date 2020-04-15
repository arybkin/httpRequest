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
	def parallelizedWork = [:]
	parallelizedWork<<Documentation()
	parallelizedWork<<OnlyUnitTests()
	parallelizedWork<<ParallelTests()//54
	parallel parallelizedWork



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
	testPlans[row] = {row}
	return testPlans
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
		return [:]
	}
}

def ParallelTests(){
	stage("ParallelTests") {
		println("log")
		return [:]
	}
}

def Documentation(){
	stage("Build Documentation"){
		CheckoutSCM()
		LoadingScripts()
		BuildDocumentation()
		AnalyzeDocumentation()
		return [:]
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
					sleep time: 60, unit: 'SECONDS'
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

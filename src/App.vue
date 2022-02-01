<template>
<Experiment title="magpie demo">
  <InstructionScreen :title="'Welcome'">
    This is a sample introduction screen.
    <br />
    <br />
    This screen welcomes the participant and gives general information about
    the experiment.
    <br />
    <br />
    This mock up experiment is a showcase of the functionality of magpie.
  </InstructionScreen>


  <!-- Here we create screens in a loop for every entry in forced_choice -->
  <template v-for="(trial, i) in trialData">
    <ForcedChoiceScreen
      :key="i"
      question="Did E pass through the gate?"
      :options="['yes', 'no']"
      >
      <template #stimulus>
        <iframe src="physics_world.html" width=800 height=600 id="physics-world-iframe"></iframe>
        <hr />

        <div id='simulation_text' style="text-align:center"><p>Please press 'Watch' to view the rest of the clip.</p></div>
        <hr />
</div>

<button type="button" class="next" id="simulate"
                @click="startScene(structure = trial.structure, block1 = true, block2 = false,time = 500, pos = 'Atop', pA = 0.2, pB = 0.8)"
        >
  Watch</button>
</template>
</ForcedChoiceScreen>
</template>


    <!--

      Comment this in, to try out interactive components like the Chat component.

      <ConnectInteractiveScreen />

      <Screen>
          <Chat :messages.sync="$magpie.measurements.messages"></Chat>
          <button @click="$magpie.saveAndNextScreen()">Next</button>
      </Screen>

      -->

    <PostTestScreen />

    <!-- While developing your experiment, using the DebugResults screen is fine,
      once you're going live, you can use the <SubmitResults> screen to automatically send your experimental data to the server. -->
    <DebugResultsScreen />
  </Experiment>
</template>

<script>
// Load data from csv files as javascript arrays with objects
import _ from 'lodash';

var trialData = [
  {structure : "disjunctive",
   block1 : true,
   block2 : false,
   time : 500,
   pos : "Atop",
   pA : 0.2,
   pB : 0.8
  },
  {structure : "conjunctive",
   block1 : true,
   block2 : false,
   time : 500,
   pos : "Btop",
   pA : 0.2,
   pB : 0.8
  },
]
export default {
  name: 'App',
  data() {
    return {
      trialData,
    };
  },
  methods: {
    startScene : function(structure, block1, block2,time,pos, pA, pB) {
      console.log("huhu haha")
      var physics_world = document.getElementById('physics-world-iframe').contentWindow;
      // $('#simulate').prop('disabled',true)
      physics_world.Start(structure = structure, block1 = block1, block2 = block2, time = time, pos = pos, pA = pA, pB = pB);
      // $('#simulate').prop('disabled',false);
}
  }
};

</script>

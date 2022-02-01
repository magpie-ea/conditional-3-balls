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
          <iframe
            id="physics-world-iframe"
            src="physics_world.html"
            width="800"
            height="600"
          ></iframe>
          <hr />

          <div id="simulation_text" style="text-align: center;">
            <p>Please press 'Watch' to view the rest of the clip.</p>
          </div>
          <hr />

          <button
            id="simulate"
            type="button"
            class="next"
            @click="
              startScene(
                (structure = trial.structure),
                (block1 = trial.block1),
                (block2 = trial.block2),
                (time = trial.time),
                (pos = trial.pos),
                (pA = trial.pA),
                (pB = trial.pB)
              )
            "
          >
            Watch
          </button>
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
import trialData from '../trials/trials.csv';

export default {
  name: 'App',
  data() {
    return {
      trialData
    };
  },
  methods: {
    startScene: function (structure, block1, block2, time, pos, pA, pB) {
      console.log('huhu haha');
      var physics_world = document.getElementById(
        'physics-world-iframe'
      ).contentWindow;
      // $('#simulate').prop('disabled',true)
      physics_world.Start(structure, block1, block2, time, pos, pA, pB);
      // $('#simulate').prop('disabled',false);
    }
  }
};
</script>

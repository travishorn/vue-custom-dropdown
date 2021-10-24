<script setup>
import { computed, ref } from "vue";
import ListBox from "./components/ListBox.vue";

const seasons = [
  { value: "2021", text: "2021" },
  { value: "2020", text: "2020" },
  { value: "2019", text: "2019" },
  { value: "2018", text: "2018" },
];

const selectedSeason = ref(seasons[0]);

const allTeams = [
  { value: "CHW", text: "Chicago White Sox", division: "AL Central"},
  { value: "CLE", text: "Cleveland Indians", division: "AL Central"},
  { value: "DET", text: "Detroit Tigers", division: "AL Central"},
  { value: "KC", text: "Kansas City Royals", division: "AL Central"},
  { value: "MIN", text: "Minnesota Twins", division: "AL Central"},
  { value: "BAL", text: "Baltimore Orioles", division: "AL East"},
  { value: "BOS", text: "Boston Red Sox", division: "AL East"},
  { value: "NYY", text: "New York Yankees", division: "AL East"},
  { value: "TB", text: "Tampa Bay Rays", division: "AL East"},
  { value: "TOR", text: "Toronto Blue Jays", division: "AL East"},
  { value: "HOU", text: "Houston Astros", division: "AL West"},
  { value: "LAA", text: "Los Angeles Angels", division: "AL West"},
  { value: "OAK", text: "Oakland Athletics", division: "AL West"},
  { value: "SEA", text: "Seattle Mariners", division: "AL West"},
  { value: "TEX", text: "Texas Rangers", division: "AL West"},
  { value: "CHC", text: "Chicago Cubs", division: "NL Central"},
  { value: "CIN", text: "Cincinnati Reds", division: "NL Central"},
  { value: "MIL", text: "Milwaukee Brewers", division: "NL Central"},
  { value: "PIT", text: "Pittsburgh Pirates", division: "NL Central"},
  { value: "STL", text: "St. Louis Cardinals", division: "NL Central"},
  { value: "ATL", text: "Atlanta Braves", division: "NL East"},
  { value: "MIA", text: "Miami Marlins", division: "NL East"},
  { value: "NYM", text: "New York Mets", division: "NL East"},
  { value: "PHI", text: "Philadelphia Phillies", division: "NL East"},
  { value: "WAS", text: "Washington Nationals", division: "NL East"},
  { value: "ARI", text: "Arizona Diamondbacks", division: "NL West"},
  { value: "COL", text: "Colorado Rockies", division: "NL West"},
  { value: "LAD", text: "Los Angeles Dodgers", division: "NL West"},
  { value: "SD", text: "San Diego Padres", division: "NL West"},
  { value: "SF", text: "San Francisco Giants", division: "NL West"},
];

// Array of unique divisions (6)
const divisions = allTeams.map((team) => {
  return { value: team.division, text: team.division };
}).filter((division, i, self) => {
  return i === self.findIndex(division2 => {
    return JSON.stringify(division) === JSON.stringify(division2);
  });
});

const selectedDivision = ref(divisions[0]);

// Return only teams who match the selected division
const teams = computed(() => {
  return allTeams.filter((team) => {
    return team.division == selectedDivision.value.value;
  });
});

const selectedTeam = ref(teams.value[0]);
</script>

<template>
  <div class="flex justify-center my-4">
    <div class="flex space-x-4">
      <ListBox :options="seasons" v-model="selectedSeason" />
      <ListBox :options="divisions" v-model="selectedDivision" />
      <ListBox :options="teams" v-model="selectedTeam" />
    </div>
  </div>

  <div class="flex justify-center">
    Showing data for
    {{ selectedSeason.text }}
    {{ selectedDivision.text }}
    {{ selectedTeam.text }}.
  </div>
</template>

<style>

</style>

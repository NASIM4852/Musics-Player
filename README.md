import { useState } from "react";
import { Play, Pause, SkipForward, Volume2 } from "lucide-react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

const songs = [
  { id: 1, title: "Song One", category: "Pop", url: "song1.mp3" },
  { id: 2, title: "Song Two", category: "Rock", url: "song2.mp3" },
  { id: 3, title: "Song Three", category: "Jazz", url: "song3.mp3" },
];

export default function MusicPlayer() {
  const [currentSong, setCurrentSong] = useState(songs[0]);
  const [isPlaying, setIsPlaying] = useState(false);
  const [volume, setVolume] = useState(50);
  const [search, setSearch] = useState("");

  const togglePlayPause = () => setIsPlaying(!isPlaying);
  const skipSong = () => {
    const currentIndex = songs.findIndex((song) => song.id === currentSong.id);
    const nextIndex = (currentIndex + 1) % songs.length;
    setCurrentSong(songs[nextIndex]);
  };

  return (
    <Card className="p-4 w-96 mx-auto text-center">
      <h2 className="text-xl font-bold mb-2">Music Player</h2>
      <Input
        placeholder="Search Songs..."
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        className="mb-2"
      />
      <CardContent>
        <h3 className="text-lg font-semibold">{currentSong.title}</h3>
        <p className="text-sm text-gray-500">{currentSong.category}</p>
        <div className="flex justify-center gap-4 mt-4">
          <Button onClick={togglePlayPause}>
            {isPlaying ? <Pause /> : <Play />}
          </Button>
          <Button onClick={skipSong}>
            <SkipForward />
          </Button>
          <Input
            type="range"
            min="0"
            max="100"
            value={volume}
            onChange={(e) => setVolume(e.target.value)}
            className="w-24"
          />
          <Volume2 />
        </div>
      </CardContent>
    </Card>
  );
}


